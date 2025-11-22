Paste this code to run.
from validate_schema_simple import validate_single_table

# Validate admissions table
validate_single_table(
    schema_file='nwicu.xlsx',
    csv_file='admissions.csv',
    table_name='admissions',
    schema_name='nw_hosp'
)
