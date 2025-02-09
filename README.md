# Livestock Insurance in Brazil

There are two data sources:
1. **SUSEP**: This is the agency that oversees the insurance industry in Brazil. They released an anonymized dataset containing all rural insurance contracts from 2006 to 2021.
    - The data can be accessed [here](https://www.gov.br/susep/pt-br/central-de-conteudos/dados-estatisticos/bases-anonimizadas/bases_rural)
    - I've translated the column names, filtered to livestock insurance and merged the files into [data/SUSEP_policies.csv](data/SUSEP_policies.csv) and [data/SUSEP_claims.csv](data/SUSEP_claims.csv)
1. **PSR** (Programa de Seguro Rural): This is a subsidy program. They publish information on all policies that received federal subsidies. The share of policies sold  that receive subsidy varies greatly by product. For livestock insurance I think roughly 30% of the policies received subsidy.
    - The data is available [here](https://dados.agricultura.gov.br/dataset/sisser3)
    - I've filtered to livestock insurance and merged the files into [data/PSR.csv](data/PSR.csv)
    - An advantage of this dataset is that it is not annonimized. You can see the farmers names and lat lon coordinates (I might not have included those columns here).


## Columns in each file

### SUSEP
Each line in the dataset is a "record". Most contracts are associated to one record, which initially added the contract to the database. Some contracts are associated to other records that modify or eliminate the contract from the database. 

| variable name | Description/notes |
| -------------- | -------------- |
| policy_cd | Contract identifier |
| record_cd | Record identifier. Most contracts have one record. Some have additional records that modify/eliminate the contract from the database. |
| item_cd | Some contracts include several "items", like different plots of land or aniamls. Most contracts have a unique item. |
| year_susep | Identifies the csv file from which this record was taken. Some policies appear in two consecutive files. These need to be cleaned. |
| record_type | Action associated to this record. 0 = Adding a policy to the database; 1 = Inclusion or rectification of an item; 2 = Modifying the policy; 3 = Cancel contract/exclude item; 4 = Cancel last record |
| fund_coverage | Whether the policy is covered by FESR (reinsurance) |
| insurance_branch | Agricultural/Livestock/etc. |
| coverage_type | See sec. 1.12 in the [documentation](https://dadosabertos.susep.gov.br/dadosabertos/rural_animais/Dados_Rural_Animais.pdf) |
| state | State (aka UF for Unidade Federativa) |
| start_date | Coverage start date |
| end_date | Coverage start date |
| deductible_type | Type of deductible. See sec. 1.15 of [documentation](https://dadosabertos.susep.gov.br/dadosabertos/rural_animais/Dados_Rural_Animais.pdf) |
| deductible_vl | Deductible value |
| insured_area | Insured area (mostly relevant for agricultural insurance) |
| insured_vl | Insured value |
| premium_vl | Premium value |
| subsidy_vl | Subsidy value |
| subsidy_source | Subsidy source. 00 if no subsidy , BR if federal insurance. Otherwise the state abbr. |
| broker_vl | Brokerage |
| markup_perc | Markup as % of the premium |
| risk_discount_perc | Additional charges for planting in risky zones |
| mun_cd_ibge | Muncipality code given by [IBGE](https://www.ibge.gov.br/explica/codigos-dos-municipios.php) |
| crop | Crop |
| firm | Firm -- Not 100% reliable |

### PSR

| variable name | Description/notes |
| -------------- | -------------- |
| psr_year | Identifies the csv file from which this record was taken |
| proposal_id | Contract identifier |
| state | State |
| mun_cd_ibge | Muncipality code |
| insuree_name | Insuree name |
| insuree_id | Insuree ID # |
| insurance_type | Insurance type (whether it covers costs or yields) |
| insured_area | Insured area |
| yield_est | Estimated yield |
| yield_insured | Insured yield |
| insured_animals | # of insured animals |
| coverage | Coverage % |
| insured_vl | Insured value ($R) |
| premium_vl | Premium value |
| subsidy_vl | Subsidy |
| premium_rate | Premium rate % |
| claim_vl | Claimed value |
| event_type | Event associated to claim |
| proposal_date | Date of subsidy proposal |
| start_date | Coverage start date |
| end_date | Coverage end date |
| policy_date | Date contract was signed |
| latitude | Latitude |
| latitude_deg | Latitude |
| latitude_min | Latitude |
| latitude_sec | Latitude |
| longitude | longitude |
| longitude_deg | longitude |
| longitude_min | longitude |
| longitude_sec | longitude |
| crop | Crop |
| firm | Firm |


## Other data sources to consider

- [Livestock production by municipality](https://sidra.ibge.gov.br/pesquisa/ppm/tabelas/brasil/2023)
- [Supply chain data in Brazil and other countries](https://trase.earth/open-data)
- I have historical weather data at the municipality level in Brazil 