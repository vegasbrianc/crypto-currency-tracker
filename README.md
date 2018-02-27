# A Crypto Currency tracker using Prometheus and Grafana

- Introduction
  - [Overview](#a-crypto-currency-tracker-using-prometheus-and-grafana)
	- [Crypto Currency Tracker Quickstart](#crypto-currency-tracker-quickstart)
  - [Pre-requisites](#pre-requisites)
  - [Installation & Configuration](#installation--configuration)
  	- [Post Configuration](#post-configuration)
  	- [Install Dashboard](#install-dashboard)
  - [Security Considerations](#security-considerations)


This is a project that utilizes [Prometheus](http://prometheus.io/), [Grafana](www.grafana.org), and the [CoinMarketCap Prometheus Exporter](https://github.com/bonovoxly/coinmarketcap-exporter).

<img src="https://raw.githubusercontent.com/vegasbrianc/crypto-currency-tracker/master/img/crypto-currency-tracker-dashboard.png" width="400" heighth="400">


## Crypto Currency Tracker Quickstart

Can't be bothered with setting up Docker to test it out? You are in luck. We created a quickstart using Play-With-Docker (PWD) to start-up the Crypto-Currency Tracker stack inside the Play-With-Docker infrastrucutre so you can try it out. This will allow you to quickly test the stack to see if it meets your needs. 

[![Try in PWD](https://github.com/play-with-docker/stacks/raw/master/assets/images/button.png)](https://labs.play-with-docker.com/?stack=https://raw.githubusercontent.com/vegasbrianc/crypto-currency-tracker/master/pwd-stack.yml) 

# Pre-requisites

Before we get started installing the Prometheus stack. Ensure you install the latest version of docker and [docker swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/) on your Docker host machine. Docker Swarm is installed automatically when using Docker for Mac or Docker for Windows.

# Installation & Configuration

Clone the project locally to your Docker host. 

If you would like to change which targets should be monitored or make configuration changes edit the [/prometheus/prometheus.yml](https://github.com/vegasbrianc/prometheus/blob/version-2/prometheus/prometheus.yml) file. The targets section is where you define what should be monitored by Prometheus. The names defined in this file are actually sourced from the service name in the docker-compose file. If you wish to change names of the services you can add the "container_name" parameter in the `docker-compose.yml` file.

Once configurations are done let's start it up. From the /prometheus project directory run the following command:

    $ HOSTNAME=$(hostname) docker stack deploy -c docker-compose.yml prom


That's it the `docker stack deploy' command deploys the entire Grafana and Prometheus stack automagically to the Docker Swarm. By default cAdvisor and node-exporter are set to Global deployment which means they will propogate to every docker host attached to the Swarm.

The Grafana Dashboard is now accessible via: `http://<Host IP Address>:3000` for example http://192.168.10.1:3000

	username - admin
	password - foobar (Password is stored in the `config.monitoring` env file)

In order to check the status of the newly created stack:
    
    $ docker stack ps prom

View running services:

    $ docker service ls

View logs for a specific service
  
    $ docker service logs prom_<service_name>

## Post Configuration

Now we need to create the Prometheus Datasource in order to connect Grafana to Prometheus 
* Click the `Grafana` Menu at the top left corner (looks like a fireball)
* Click `Data Sources`
* Click the green button `Add Data Source`.

<img src="https://github.com/vegasbrianc/prometheus/raw/version-2/images/Add_Data_Source.png" width="400" heighth="400">

## Install Dashboard
I updated the projects Dashboard to add a little bit more flair. You can have a look at the dashboard [Grafana Docker Dashboard](https://grafana.net/dashboards/4893) Simply download the dashboard and select from the Grafana menu -> Dashboards -> Import and use the Dashboard ID `4893`

The original project creator [bonovoxly](https://twitter.com/bonovoxly) created a nice dashboard available on [Grafana Docker Dashboard](https://grafana.net/dashboards/3890). Simply download the dashboard and select from the Grafana menu -> Dashboards -> Import and use the Dashboard ID `3890`

<img src="https://raw.githubusercontent.com/vegasbrianc/crypto-currency-tracker/master/img/crypto-currency-tracker-dashboard.png" width="400" heighth="400">

# Security Considerations
This project is intended to be a quick-start to get up and running with Docker and Prometheus. Security has not been implemented in this project. It is the users responsability to implement Firewall/IpTables and SSL.

Since this is a template to get started Prometheus and Alerting services are exposing their ports to allow for easy troubleshooting and understanding of how the stack works.
