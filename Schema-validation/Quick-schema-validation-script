#!/usr/bin/env python3
"""
Quick Schema Validation Script
Simplified version for interactive use
"""

import pandas as pd
import numpy as np
import re
from pathlib import Path


def validate_single_table(schema_file, csv_file, table_name, schema_name='nw_hosp'):
    """Quick validation for a single table"""
    
    # Load schema
    schema_df = pd.read_excel(schema_file) if schema_file.endswith('.xlsx') else pd.read_csv(schema_file)
    
    # Load CSV data
    print(f"Loading CSV: {csv_file}")
    df = pd.read_csv(csv_file, low_memory=False)
    print(f"Rows: {len(df):,}, Columns: {len(df.columns)}")
    
    # Get schema for this table
    table_schema = schema_df[
        (schema_df['Schema'] == schema_name) & 
        (schema_df['Table'] == table_name)
    ]
    
    print(f"\n{'='*80}")
    print(f"VALIDATION REPORT: {schema_name}.{table_name}")
    print(f"{'='*80}\n")
    
    issues = []
    recommendations = []
    
    for idx, row in table_schema.iterrows():
        variable = row['Variable']
        type_str = row['Type']
        
        if variable not in df.columns:
            issues.append(f"❌ Column '{variable}' missing from CSV")
            continue
        
        column_data = df[variable]
        
        # Parse type
        not_null = 'NOT NULL' in str(type_str).upper()
        
        # Check NOT NULL violations
        if not_null:
            null_count = column_data.isna().sum()
            if null_count > 0:
                pct = (null_count / len(df) * 100)
                issues.append(f"⚠️  {variable}: {null_count:,} NULL values ({pct:.2f}%) but defined as NOT NULL")
        
        # Check VARCHAR/CHAR lengths
        varchar_match = re.search(r'(VARCHAR|CHAR)\((\d+)\)', str(type_str), re.IGNORECASE)
        if varchar_match:
            defined_length = int(varchar_match.group(2))
            
            # Calculate actual max byte length
            valid_values = column_data.dropna().astype(str)
            if len(valid_values) > 0:
                max_bytes = valid_values.apply(lambda x: len(x.encode('utf-8'))).max()
                utilization = (max_bytes / defined_length * 100)
                
                if max_bytes > defined_length:
                    issues.append(f"❌ {variable}: Max length {max_bytes} exceeds defined {defined_length}")
                    issues.append(f"   Suggested: VARCHAR({max_bytes + 10})")
                    
                    # Show examples
                    longest_idx = valid_values.apply(lambda x: len(x.encode('utf-8'))).idxmax()
                    example = valid_values.loc[longest_idx]
                    issues.append(f"   Example: '{example[:50]}...'")
                    
                elif utilization < 50 and defined_length > 50:
                    recommendations.append(f"💡 {variable}: Using {utilization:.1f}% of VARCHAR({defined_length}), could reduce to VARCHAR({max_bytes + 10})")
        
        # Check INTEGER types
        int_match = re.search(r'(SMALLINT|INTEGER|BIGINT)', str(type_str), re.IGNORECASE)
        if int_match:
            int_type = int_match.group(1).upper()
            valid_values = pd.to_numeric(column_data.dropna(), errors='coerce').dropna()
            
            if len(valid_values) > 0:
                min_val = valid_values.min()
                max_val = valid_values.max()
                
                # Check ranges
                if int_type == 'SMALLINT' and (min_val < -32768 or max_val > 32767):
                    issues.append(f"❌ {variable}: Values ({min_val} to {max_val}) exceed SMALLINT range")
                elif int_type == 'INTEGER' and (min_val < -2147483648 or max_val > 2147483647):
                    issues.append(f"❌ {variable}: Values ({min_val} to {max_val}) exceed INTEGER range")
                
                # Suggest optimization
                if int_type in ['INTEGER', 'BIGINT'] and min_val >= -32768 and max_val <= 32767:
                    recommendations.append(f"💡 {variable}: Could use SMALLINT instead of {int_type} (range: {min_val} to {max_val})")
    
    # Print results
    if issues:
        print("ISSUES FOUND:")
        print("─" * 80)
        for issue in issues:
            print(issue)
        print()
    
    if recommendations:
        print("OPTIMIZATION RECOMMENDATIONS:")
        print("─" * 80)
        for rec in recommendations:
            print(rec)
        print()
    
    if not issues and not recommendations:
        print("✅ No issues found! Schema looks good.")
    
    print(f"\n{'='*80}\n")
    
    return len(issues), len(recommendations)


def analyze_actual_data_characteristics(csv_file, sample_size=10000):
    """Analyze CSV file to suggest optimal data types"""
    
    print(f"Analyzing data characteristics: {csv_file}\n")
    
    df = pd.read_csv(csv_file, nrows=sample_size, low_memory=False)
    
    suggestions = []
    
    for col in df.columns:
        col_data = df[col]
        null_pct = (col_data.isna().sum() / len(col_data) * 100)
        
        suggestion = {
            'column': col,
            'null_pct': round(null_pct, 2),
            'not_null_safe': null_pct == 0
        }
        
        # Analyze non-null values
        valid_data = col_data.dropna()
        
        if len(valid_data) == 0:
            suggestion['type'] = 'All NULL - cannot determine'
            suggestions.append(suggestion)
            continue
        
        # Try to infer type
        # Check if numeric
        numeric_data = pd.to_numeric(valid_data, errors='coerce')
        numeric_ratio = numeric_data.notna().sum() / len(valid_data)
        
        if numeric_ratio > 0.9:  # Mostly numeric
            # Check if integer
            if (numeric_data == numeric_data.astype(int, errors='ignore')).all():
                min_val = numeric_data.min()
                max_val = numeric_data.max()
                
                if min_val >= -32768 and max_val <= 32767:
                    suggestion['type'] = 'SMALLINT'
                elif min_val >= -2147483648 and max_val <= 2147483647:
                    suggestion['type'] = 'INTEGER'
                else:
                    suggestion['type'] = 'BIGINT'
                
                suggestion['range'] = f"{min_val} to {max_val}"
            else:
                suggestion['type'] = 'FLOAT or DOUBLE PRECISION'
        else:
            # String data
            str_data = valid_data.astype(str)
            max_len = str_data.apply(lambda x: len(x.encode('utf-8'))).max()
            avg_len = str_data.apply(lambda x: len(x.encode('utf-8'))).mean()
            
            suggested_len = int(max_len * 1.2)  # 20% buffer
            
            suggestion['type'] = f"VARCHAR({suggested_len})"
            suggestion['max_length'] = max_len
            suggestion['avg_length'] = round(avg_len, 1)
        
        suggestions.append(suggestion)
    
    # Print suggestions
    print(f"{'Column':<30} {'Suggested Type':<25} {'NULL%':<8} {'Details'}")
    print("─" * 100)
    
    for s in suggestions:
        details = ""
        if 'range' in s:
            details = f"Range: {s['range']}"
        elif 'max_length' in s:
            details = f"Max: {s['max_length']}, Avg: {s['avg_length']}"
        
        not_null = " (NOT NULL safe)" if s['not_null_safe'] else ""
        
        print(f"{s['column']:<30} {s['type']:<25} {s['null_pct']:<8.2f} {details}{not_null}")
    
    return suggestions


# Example usage
if __name__ == '__main__':
    print("""
╔══════════════════════════════════════════════════════════════════════════════╗
║                     NWICU Schema Validation Tool                             ║
╚══════════════════════════════════════════════════════════════════════════════╝

This script provides two modes:

1. VALIDATE MODE: Check existing schema against CSV data
2. ANALYZE MODE: Suggest optimal schema from CSV data

""")
    
    # Example for validate mode:
    # validate_single_table('nwicu.xlsx', 'admissions.csv', 'admissions', 'nw_hosp')
    
    # Example for analyze mode:
    # analyze_actual_data_characteristics('admissions.csv')
    
    print("To use this script:")
    print("  from validate_schema_simple import validate_single_table, analyze_actual_data_characteristics")
    print()
    print("  # Validate existing schema")
    print("  validate_single_table('nwicu.xlsx', 'your_data.csv', 'table_name', 'schema_name')")
    print()
    print("  # Analyze data to suggest schema")
    print("  analyze_actual_data_characteristics('your_data.csv')")
