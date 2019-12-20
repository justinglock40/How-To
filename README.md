# How-To's 

All credit to BenderTwin (Donate:) https://beerpay.io/benderstwin/benders-scripts

Simple Tutorial for deploying Varken, Influx, Telegraf, Grafana. For further customization and panel configuration help, please reach out to PTS Community. 

Sensible order of installation:

1. Influx
2. Telegraf
3. Varken
4. Grafana

Deploy influxdb, grafana, and varken in PTS Community Apps

Edit your Varken.ini file **`sudo nano /opt/appdata/varken/varken.ini`**

Instructions to configure varken.ini are not part of this howto but are located here **https://github.com/Boerderij/Varken/wiki/Configuration** 

Use the container name for anything on the same host (i.e., tautulli,influx, ombi, sonarr, radarr, lidarr etc...)

Now go to **https://grafana.yourdomain.com**. Default Username and Password are admin/admin

Highly recommended that you change the default Grafana password:

Add influxdb as a datasource in Grafana URL is **http://influxdb:8086**

Database is **varken**

Username = **admin** 

password = **adminpass**

Import dashboard - **https://grafana.com/dashboards/9585**

Install dependency plugins: **`sudo docker exec -it grafana /bin/bash paste in grafana-cli plugins install grafana-piechart-panel and grafana-cli plugins install grafana-worldmap-panel`**

Restart the container **`sudo docker restart grafana`**

**HOW TO SET UP TELEGRAF ON PTS**

Do all of the following as root, or using sudo

*Create the directory /opt/appdata/telegraf*
**`sudo mkdir /opt/appdata/telegraf`**

*Change to the telegraf directory and download config*

**`cd /opt/appdata/telegraf`**

**`wget https://raw.githubusercontent.com/benderstwin/PlexGuide-Community/v8.4/apps/telegraf.conf`**

*edit the telegraf.conf to add influxdb username and password*

**`nano -c /opt/appdata/telegraf.conf`**

- tip: adding the -c to the nano command will show you the line number at the bottom, makes it easier to find.
Look for these lines (around line 116) under `HTTP Basic Auth`

    **username = "admin"**
    **password = "adminpass"**
    
**`Ctrl+ O`** to save the file.

**Deploy Telegraf in PTS Community Apps**

Add the datasource to grafana, import or create a dashboard, profit. When you add the data source, the URL is **http://influxdb:8086** and the db name will be **telegraf** (database should be created for you already)
