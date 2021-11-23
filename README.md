
# HDV Emissions - Data Parser

This project focuses on the data provided by the [EEA](https://www.eea.europa.eu/data-and-maps/data/co2-emission-hdv).

The data is exposed via a [web app](https://discomap.eea.europa.eu/app/CO2HDV/#) with a download limit of
300,000 rows at a time, however there are > 1 million.

The full dataset is available from `https://discomap.eea.europa.eu/app/CO2HDV/CO2EmissionHDV_VehicleExtract_02062021.zip`.

## API 
The web app is backed by an API that enables us to interact with the data programmatically as follows:

To get the filter data (used below) we make a GET request to: `https://discomap.eea.europa.eu/app/CO2HDV/init`

### Response Payload:
```json
{
    "Config": {...},
    "Request": {...},
    "Response": {
        "Fields": {
            "Make": {
                "DomainStats": true,
                "FieldName": "Make",
                "PossibleValues": [
                    {"Value": "ISUZU", "NumRecords": 90},
                    {"Value": "IVECO", "NumRecords": 19277},
                    ...
                ]
            },
            "Manufacturer": {
                "DomainStats": true,
                "FieldName": "Manufacturer",
                "PossibleValues": [
                    {"Value": "null", "NumRecords": 1012820},
                    {"Value": "Daimler AG", "NumRecords": 40144},
                    ...
                ]
            },
    }
}
```

To get a download link we make a POST request to: `https://discomap.eea.europa.eu/app/CO2HDV/download?f=csv`

### Request Payload:
```json
{
    "Page": 0,
    "SortBy": "",
    "SortAscending": true,
    "RequestFilter": {
        "Make": {
            "FieldName": "Make",
            "Values": [
                "IVECO"
            ]
        }
    }
}
```
TODO: Not fully sure how this type of download stream is handled programmatically but I don't think it'll be an issue. 






