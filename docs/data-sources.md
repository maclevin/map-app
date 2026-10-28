# Data sources (verified Oct 27, 2026)

## Address to coordinates
NJ Geocode service: `https://geo.nj.gov/arcgis/rest/services/Tasks/NJ_Geocode/GeocodeServer/findAddressCandidates`
- Params: `SingleLine`, `outFields=*`, `outSR=4326`, `f=json`
- Attributes include `Subregion` (county), `Zone` (municipality), `Addr_Block`, `Addr_Lot`, `Addr_Qualifier`
- Allows cross-origin requests

## Parcels and tax list (deed book and page)
NJOGIS Parcels and MOD-IV Composite: `https://maps.nj.gov/arcgis/rest/services/Framework/Cadastral/MapServer/0/query`
- Key fields: `PAMS_PIN`, `PCL_MUN` (e.g. 1510 = Harvey Cedars Boro), `PCLBLOCK`, `PCLLOT`, `PCLQCODE`, `PROP_LOC`, `DEED_BOOK`, `DEED_PAGE`, `DEED_DATE` (YYMMDD, appears to be the date signed, not recorded), `SALE_PRICE`, `LAND_DESC`, `CALC_ACRE`, `ADD_LOTS1/2`
- `OWNER_NAME` is blank in the public data
- A point query finds the lot; a polygon query with `distance=2` (feet) finds adjoiners (POST, form-encoded)
- Sub-lots such as riparian lots (e.g. 2.01) have geometry but no tax record
- `maxRecordCount` is 1000. Distinct-value queries are slow (~6 s), so the 33 Ocean County municipality codes are hard-coded

## Recorded deeds: Ocean County Clerk
Free search: `https://sng.co.ocean.nj.us/searchapplication/` → "Free Search" (accept disclaimer) → `https://sng.co.ocean.nj.us/publicsearch/`
- Records online from April 1, 1977. Search by party, document type, instrument number, book/page, town/lot/block, case/parcel
- Page images are free to view and watermarked as unofficial
- Each document has a direct viewer link: `https://sng.co.ocean.nj.us/publicsearch/viewer.aspx?docID=<id>`; the id is only known after a search
- The site's search and document calls are protected by reCAPTCHA. The app must not call them; it hands off to the Clerk's site for a person to open. Full automation needs a data agreement with the Clerk or a licensed records vendor.

## Known limits
- Pages hosted inside Claude cannot reach the state servers; run `index.html` locally in a browser
- Curved courses are flagged in the plotter but not drawn yet
