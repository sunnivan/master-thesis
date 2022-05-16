# master-thesis
A collection of all code used to produce the results for my master thesis.

# Contents
This README.md file will contain brief explanation of what each notebook in this repository does, 
and the order of how they fit together. Each notebook contain short notices on what is done before relevant code cells.

# Packages used
* cartopy
* decartes
* geopandas
* glob
* json
* matplotlib
* numpy
* os 
* pandas
* pymannkendall
* re
* regionmask
* requests
* shapely
* sklearn
* treeinterpreter
* xarray

# regionmask.ipynb

regionmask.ipynb is a notebook made to take in a list of catchment names (defined by NVE) and assign each the
shapefile corresponding to the catchment name. The catchment shapefile is then used to create a mask using regionmask.
Catchment shapefiles can be downloaded using NVE's map services https://nedlasting.nve.no/gis/

# lese_senorge.ipynb

lese_senorge.ipynb contains a function used to read netcdf-files covering the whole of Norway on a 1x1km grid, and mask 
them through the catchment masks made in regionmask.ipynb. This results in csv-files (one per year) containing only data for grid cells
within the catchment masks.

# csv_til_csv.ipynb
csv_til_csv.ipynb takes the yearly files made in lese_senorge.ipynb and combines them to one csv-file.

# plot_catchment_map.ipynb
plot_catchment_map.ipynb uses shapefiles from NVE's map services https://nedlasting.nve.no/gis/ and 
Natural Earth data https://www.naturalearthdata.com/downloads/10m-cultural-vectors/ and makes a map of Norway's outline,
with its runoff regions and selected catchments within.

# hente_dc.ipynb and hente_cc.ipynb
Both these files use the Norwegian Water Resources and Energy Directorate's hydrological database HydAPI to collect data,
https://hydapi.nve.no/UserDocumentation. 
hente_dc.ipynb collects discharge data for a selection of catchments. hente_cc.ipynb collects a selection of
catchment characteristics belonging to the selected catchments. 

# snow_var.ipynb
snow_var.ipynb uses snow and evaporation data run through lese_senorge.ipynb. It calculates mean yearly value for each
of the catchments, before it calculates the trends over the period 01.01.1991-31.12.2019 for each of the snow and evaporation values. 

# my_dc_dataset.ipynb
my_dc_dataset.ipynb first use the collected discharge data from hente_dc.ipynb to calculate mean annual discharge and 
seasonal high and low flow in the period 01.01.1991-31.12.2019. Then trends are calculated for these variables. Trends are 
added to a dataframe, together with the catchment characterisitcs from hente_cc.ipynb, mean values and trends calculated
in snow_var.ipynb as well as mean values and trends in precipitation and temperature for each catchment. The dataframe
containing all values is saved. The trends in mean annual discharge and high and low flow are plotted into maps, using 
roughly the same method as in plot_catchment_map.ipynb, with some additions. Catchment characteristics, snow, 
evaporation, temperature and precipitation is also plotted.

# heatmap.ipynb
heatmap.ipynb uses the saved Dataframe from my_dc_dataset.ipynb to plot all calculated discharge trends, both annual and
seasonal into one figure.

# start_ML.ipynb
start_ML.ipynb uses the saved Dataframe from my_dc_dataset.ipynb to first make a correlation matrix of all its contents.
Then the machine learning method decision tree is applied to chosen target variables. The non-target variables in the table 
are used as explanation variables. Feature importances for each predicted tree is stored.

# random_forest.ipynb
random_forest.ipynb uses the saved Dataframe from my_dc_dataset.ipynb to apply the machine learning method random forest
on chosen target variables. The non-target variables in the table are used as explanation variables. Feature importances for 
each prediction is stored. Then the feature importance lists from start_ML.ipynb is imported into the notebook to combine both
feature importances into one plot for each target variabel.



