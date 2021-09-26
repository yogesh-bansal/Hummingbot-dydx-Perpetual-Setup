# Hummingbot for Custom Trading Strategies on dydx

The open-source Hummingbot software allows for the definition, implementation, and execution of customized market and trading strategies on a number of platforms. Recently, Hummingbot added support for the dydx platform, allowing for these trading strategies to be performed directly on the dydx platform automatically. In this blog, we will walk through the setup and configuration of Hummingbot, and show how to use it to define and execute a market strategy on dydx.

## Hummingbot Installation

Check out the end of the Readme for the [YouTube Video](https://www.youtube.com/watch?v=F6dsHxpkwGY) explaining all the installation and configurations steps in detail. Or follow the below instructions.

There are several supported installation methods for Hummingbot, including installation via Docker. For a full breakdown of the options, please see the official documentation:

- [https://docs.hummingbot.io/installation/linux/](https://docs.hummingbot.io/installation/linux/)  

In this blog, we will assume a manual installation on **Ubuntu 20.04**.

### Installing Miniconda

![](images/1.png)

- `sudo apt update`
- `sudo apt install -y build-essential`
- `wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86\_64.sh`
- `sh Miniconda3-latest-Linux-x86\_64.sh`

At this stage, you will be presented with several options dictating the installation of Miniconda. In most cases, the defaults should suffice. Running the bash script to complete the Miniconda installation may take several minutes. Once the installation is complete, we need to reload Bash in order to detect Miniconda. Simply run:

- `exec bash`

Now, we are ready to proceed by installing Hummingbot.

![](images/2.png)

### Installing Hummingbot

- `git clone https://github.com/CoinAlpha/hummingbot.git`
- `cd hummingbot && ./clean && ./install`
- `conda activate hummingbot && ./compile`

These steps, particularly cloning the repository and compiling the source code, can take a few minutes to complete. This will ensure that the conda environment is activated, and hummingbot is ready to be executed.

### Running Hummingbot

To run Hummingbot, we simply need to execute the following command:

- `bin/hummingbot.py`

You should be presented with this screen if everything worked as expected:

![](images/3.png)

Now we are ready to begin implementing our trading strategy!

## Interacting with dydx

We are now ready to begin interacting and trading on the dydx platform using Hummingbot! To begin, we need to obtain credentials from the dydx site. The API key and Stark keys are the values needed from the platform. At startup, Hummingbot requests that we create a password to secure the data. After defining and re-entering the password, you are presented with the main screen from which we simply need to choose dydx\_perpetual as our protocol, and then we can begin interacting with the platform.

![](images/hummingbot.png)

We can run `help` in order to display a list of possible commands. The one we are looking for is `connect`. The API key, secret, and passphrase from the dydx platform are required to be provided at this stage (Check the video demo at the end of the Readme to view the full process). After entering these values, you should see that the keys have been added and confirmed for dydx_perpetual, and we are good to go.

![](images/Demo.gif)

At this point, we have everything needed to begin making trades. We supply a number of strategy parameters as requested by Hummingbot. The strategy is saved as a structured YAML file, which can be read in plain text and parsed as needed to read in elements of that strategy. When we execute the strategy, immediately the trades are performed if the criteria is met. For example, we can define a strategy that says:

- Use BTC-USD as the pair of interest
- Use 25x leverage
- Use the one-way position mode (instead of hedge)
- Place the first bid order when 1% away from the mid price
- Cancel and replace bids and asks every 5 seconds
- Use .001 BTC per order
- When 1% from entry price, place stop loss order

Hummingbot guides you through all the possible choices. Once complete, and the strategy has been defined, you can go on the dydx platform, and if the conditions are met, you will immediately see your trades being executed!

## Video Tutorial

A full tutorial of the setup process, and the strategy making procedure, is given below:

[![Alt text](images/dydx.gif)](https://www.youtube.com/watch?v=F6dsHxpkwGY)
