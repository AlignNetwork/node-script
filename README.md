<h2 align="center">Align Network (⌐🔷_🔷) Node</h2>
<p align="center">

<br/>
<a href="https://twitter.com/align_network">Twitter</a>
<a href="https://warpcast.com/~/channel/align">Warpcast</a>
  
</p>

This repo is provided to run an [Arbitrum Orbit](https://docs.arbitrum.io/node-running/how-tos/running-a-full-node) full node on the Align Network. Align uses Arbitrum Orbit and rolls up to Ethereum. Our sequencer is run by Caldera, currently in testnet.

### Why run a full node?

1. Helps to provide alternative RPC's and network access outside of the teams RPCs
2. Validation: Logs an error if the L1 block posted doesn't match the local state

### Node Explained

This node is a [feed node](https://docs.arbitrum.io/node-running/how-tos/running-a-feed-relay) that connects to the Align sequencer at [wss://align-testnet.rpc.caldera.xyz/feed](wss://align-testnet.rpc.caldera.xyz/feed). It's running in [watchtower](https://docs.arbitrum.io/node-running/how-tos/running-a-validator) mode allowing it to achieve step 2 above.

### A note about BOLD

Notably this node does not challenge invalid rollup state transitions, it just alerts of them. That process is handled via [OffchainLabs' BOLD](https://github.com/OffchainLabs/bold). We'll provide further upgrades to implement BOLD so validators can actively see the state root before it's posted, allowing finality to match that of Ethereum L1. Read more about [BOLD](https://medium.com/offchainlabs/bold-permissionless-validation-for-arbitrum-chains-9934eb5328cc)

### Self Hosting

> [!IMPORTANT]  
> Unrefined steps to get this node working on AWS

This repo offers a simple docker-compose.yml file anyone can use alongside the config/nodeConfig.json file to run the node. This can be run on an AWS EC2 instance, but with significant overhead. We will be updating with simpler instructions, this code is provided as a launching point if anyone wants to launch a node.

Some brief steps to run the node:

1. Create an EC2 ubuntu instance
2. Ensure AWS has inbound rules set for your SSH, 443 and 80, allowing all outbound.
3. Add the example nginx server to your http setup at `/etc/nginx/nginx.conf` at [nginx.example.conf](/nginx.example.conf)
4. Optionally connect a url to the instance
5. Run Certbot if you'd like ssl certifications
6. git clone the repo into the instance
7. Run docker-compose up -d

Reference: [Arbitrum Nitro, Running a full node](https://docs.arbitrum.io/node-running/how-tos/running-a-full-node) if you run into trouble.

### Acknowledgements

This code was forked from [https://github.com/OffchainLabs/orbit-setup-script](https://github.com/OffchainLabs/orbit-setup-script).
