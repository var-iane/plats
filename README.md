# Phantom plats

I was panning around Google Maps satellite view one day when I came across a bunch of [fake-looking suburban roads in Texas](https://www.google.com/maps/@31.6944298,-106.1154776,9601m/data=!3m1!1e3?entry=ttu&g_ep=EgoyMDI2MDkyMy4wIKXMDSoASAFQAw%3D%3D) -- but nothing was built there. When I zoomed in far enough, the roads [had full-on names](https://www.google.com/maps/@31.6692652,-106.0668163,3710m/data=!3m1!1e3?entry=ttu&g_ep=EgoyMDI2MDkyMy4wIKXMDSoASAFQAw%3D%3D). 

I dug into the history of this tract of land, called Horizon City (and in the process learned about similar land speculation schemes with fake road grids like [California City](https://www.google.com/maps/@35.1930119,-117.7823107,9276m/data=!3m1!1e3?entry=ttu&g_ep=EgoyMDI2MDkyMy4wIKXMDSoASAFQAw%3D%3D) in the Mohave Desert and [Golden Gate Estates](https://www.google.com/maps/@26.0940478,-81.5276768,16132m/data=!3m1!1e3?entry=ttu&g_ep=EgoyMDI2MDkyMy4wIKXMDSoASAFQAw%3D%3D) in the Florida Everglades). After analyzing parcel data of a few of these places, I discovered that Horizon City's undeveloped parcels had pretty odd owners--mostly out-of-state and international--and wanted to see if I could find something interesting in the ownership data.

Goals with this project: learn how to design something responsive/for mobile(!!), get better at CSS and GSAP animations, make it as cinematic as possible

## Data sources
_Parcels_: El Paso County data from [Regrid](https://regrid.com/)'s Data with Purpose initiative

_Building footprints_: Overture Maps via `city2graph`

_Roads_: ESRI (had the most comprehensive network of platted/unpaved roads compared to TIGER/Line or Overture)

## Owner residence analysis
### Geocoding
US owner mailing addresses geocoded with `pgeocode`. International owner geocoding still in progress (mailing addresses are all over the place for these--no standard country, zip, city formats)
### Owner clusters
DBSCAN clustering with `scikit-learn` to determine geographic clusters of owners (see `02_clustering.ipynb` for parameters). Once clusters were assigned, I could color-code them in QGIS and compare against the subdivision/unit map

## Reference maps
### Subdivision/unit map
I needed an accurate subdivision/unit map to look for any relationship between owner residence and lot location. Georeferencing turned out not to be accurate enough, so I ended up hand-tracing [this unit map](https://static1.squarespace.com/static/5bae636ee8ba44ab215d2340/t/5bb3cd6a652dea9d64f16cf8/1538510190046/Overview.jpg) from the [HCIA website](https://www.horizoncommunities.com/maps-links) in vector software

### Water lines map
Traced from [here](https://static1.squarespace.com/static/5bae636ee8ba44ab215d2340/t/5bb283bde79c70974eaa4050/1538425793019/Water-Sewage-Map2.jpg), also from the [HCIA website](https://www.horizoncommunities.com/maps-links)

### Vintage marketing map
Made in Illustrator to mimic the look of a real Horizon City ad, from [this reddit post](https://www.reddit.com/r/ElPaso/comments/1i3zz76/ghost_lots_of_horizon_city/)

## Other references
_Federal Trade Commission decision against Horizon Corp_: documents [1](https://www.ftc.gov/sites/default/files/documents/commission_decision_volumes/volume-97/ftc_volume_decision_97_january_-_june_1981pages_464-563.pdf), [2](/files/documents/commission_decision_volumes/volume-97/ftc_volume_decision_97_january_-_june_1981pages_668-770.pdf), [3](lt/files/documents/commission_decision_volumes/volume-97/ftc_volume_decision_97_january_-_june_1981pages_771-911.pdf). This is where I found evidence for sales tactics (dinner parties, door-to-door, cold calls) and sales reps selling limited inventory in batches.

## Things left to do
I'd like to make an explorable version of the parcel data (owner mailing address city/state/country only), probably using PMTiles + MapLibre or something similar