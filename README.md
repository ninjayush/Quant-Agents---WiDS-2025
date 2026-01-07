The requirements.txt file contains a list of all the packages in the current environment, and their respective versions. You can re-create the environment to install the same packages using the same versions:

$ pip install -r requirements.txt

# Quant-Agents---WiDS-2025
The core of this project is to model a simulated market environment populated by multiple Quant Agents. Unlike traditional financial models, the focus is on the strategic interactions and competition among these agents.

This project is divided into several distinct phases to ensure a structured and manageable development process.

##Phase 1: Core Infrastructure and Market Setup
To get a handle on the market structure, the next logical step is to build a model for it. I'm using the Mesa Python framework for this project. Mesa is a great choice for setting up multi-agent simulations and really digging into how they all interact. Here, I have 2 models: one in a 2d grid and the other is random trading- both based on the Boltzmann wealth model. They ultimately demonstrate how wealth inequality can emerge even if you start with the same amount of money.

##Phase 2: Game Theory Strategies
In the standard Boltzmann Wealth Model, wealth is exchanged randomly. To make the model more realistic, I have explored coupling it with Game Theory, where agents make decisions based on the behavior of others rather than just "colliding" like gas particles.

1. Tit-for-Tat (Reciprocal Trading)
Understanding: Tit-for-Tat is a strategy based on reciprocity. In this version of the market model, agents are no longer anonymous; they remember their previous transaction partner.

The Logic: An agent starts by cooperating (trading). In subsequent encounters with the same partner, the agent simply copies the partner's previous move. If the partner refused to trade last time, the agent "punishes" them by refusing this time.

Impact on Model: This shifts the wealth distribution from a purely random exponential curve to one defined by social capital. Wealth tends to circulate within "high-trust" clusters, while "selfish" agents who refuse to trade eventually find themselves isolated from the wealth flow.

2. Hawk-Dove (Competitive Resource Acquisition)
Understanding: This strategy models the risk and cost of aggressive competition in a market. When two agents meet to "trade," they choose to be either a Hawk (aggressive) or a Dove (cooperative).

The Logic: * If two Doves meet, they share the wealth equally.

If a Hawk meets a Dove, the Hawk takes the entire unit of wealth.

If two Hawks meet, they compete, resulting in a "fight" where both agents lose wealth (representing legal fees, war, or market friction).

Impact on Model: Unlike the standard Boltzmann model where total wealth is conserved, the Hawk-Dove coupling introduces systemic loss. Because Hawk-Hawk interactions destroy wealth, the simulation can show how aggressive market strategies can lead to an overall economic decline despite individual agents attempting to maximize their own gain.

