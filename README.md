# A Crypto Currency tracker using Prometheus and Grafana

- Introduction
  - [Overview](#a-crypto-currency-tracker-using-prometheus-and-grafana)
	- [Crypto Currency Tracker Quickstart](#crypto-currency-tracker-quickstart)
  - [Pre-requisites](#pre-requisites)
  - [Installation & Configuration](#installation--configuration)
    - [Check Stack Status](#check-status)
  	- [Grafana Configuration](#grafana-configuration)
  	- [Install Dashboard](#install-dashboard)
  - [Security Considerations](#security-considerations)


This is a project that utilizes [Prometheus](http://prometheus.io/), [Grafana](www.grafana.org), and the [CoinMarketCap Prometheus Exporter](https://github.com/bonovoxly/coinmarketcap-exporter).

<img src="https://raw.githubusercontent.com/vegasbrianc/crypto-currency-tracker/master/img/crypto-currency-tracker-dashboard.png" width="600" heighth="400">


## Crypto Currency Tracker Quickstart

Can't be bothered with setting up Docker to test it out? You are in luck. We created a quickstart using Play-With-Docker (PWD) to start-up the Crypto-Currency Tracker stack inside the Play-With-Docker infrastrucutre so you can try it out. This will allow you to quickly test the stack to see if it meets your needs. 

[![Try in PWD](https://github.com/play-with-docker/stacks/raw/master/assets/images/button.png)](https://labs.play-with-docker.com/?stack=https://raw.githubusercontent.com/vegasbrianc/crypto-currency-tracker/master/pwd-stack.yml) 

# Pre-requisites

Before we get started installing the Prometheus stack. Ensure you install the latest version of docker and [docker swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/) on your Docker host machine. Docker Swarm is installed automatically when using Docker for Mac or Docker for Windows.

# Installation & Configuration

Clone the project locally to your Docker host. 

Change to the `crypto-currency-tracker` directory and run the following command:

    $ HOSTNAME=$(hostname) docker stack deploy -c docker-compose.yml crypto

That’s it the docker stack deploy command deploys the entire Docker, Prometheus, Grafana and CoinMarketCap stack automagically to the Docker Swarm. 
Wait a minute for everything to download and install


## Check the Status

In order to check the status of the newly created stack:
  
    $ docker stack ps crypto

View running services:
    
    $ docker service ls

View logs for a specific service

    $ docker service logs crypto_<service_name>

## Grafana Configuration

The Grafana Dashboard is now accessible via: `http://<Host IP Address>:3000` for example http://192.168.10.1:3000

    username - admin
    password - foobar (Password is stored in the `config.monitoring` env file)

Now we need to create the Prometheus Datasource in order to connect Grafana to Prometheus 
* Click the `Grafana` Menu at the top left corner (looks like a fireball)
* Click `Data Sources`
* Click the green button `Add Data Source`

Add the datasource exactly as the screenshot below:

<img src="https://github.com/vegasbrianc/prometheus/raw/version-2/images/Add_Data_Source.png" width="600" heighth="400">

## Install Dashboard
I updated the projects Dashboard to add a little bit more flair. You can have a look at the dashboard [Grafana Docker Dashboard](https://grafana.net/dashboards/4893) To install, simply import the dashboard and select from the Grafana menu -> Dashboards -> Import and use the Dashboard ID `4893 and select `prometheus` as the datasource.

The original project creator [bonovoxly](https://twitter.com/bonovoxly) created a nice dashboard available on [Grafana Docker Dashboard](https://grafana.net/dashboards/3890). Simply download the dashboard and select from the Grafana menu -> Dashboards -> Import and use the Dashboard ID `3890`

<img src="https://raw.githubusercontent.com/vegasbrianc/crypto-currency-tracker/master/img/crypto-currency-tracker-dashboard.png" width="600" heighth="400">

# Security Considerations
This project is intended to be a quick-start to get up and running monitoring Crypto Currencies with Docker, Prometheus, and Grafana. Security has not been implemented in this project. It is the users responsibility to implement Firewall/IpTables, SSL, and access control.

Since this is a template to get started Prometheus and Alerting services are exposing their ports to allow for easy troubleshooting and understanding of how the stack works.
