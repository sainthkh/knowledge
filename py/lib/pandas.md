# pandas

## DataFrame

```py
from pandas import DataFrame

# column name: values
company = { 
    'code': ('005930', '066570', '017670'), 
    'code_name': ('samsung', 'LG', 'SK'),
    'close': ('55200', '71000', '234000')
}

df_company = DataFrame(company)
df_company2 = DataFrame(company, columns=['close', 'code', 'code_name'])

df_company.iloc[0, 0]
df_company.loc[0, 'code']
```