---
title: Click on the token you want to add
tags: [metamask, wallet]
---

{% for item in site.data.tokens %}
{% assign token = item[1] %}

<div class="buttonWrapper">
    <button class="add{{token.name}}" type="button">Add
            <span>${{ token.name }}</span> to your
            <span>wallet</span>
        </button>
</div>
<script>
        document.querySelector('.add{{ token.name }}').addEventListener('click', (e) => {
            e.preventDefault();
            if (!window.ethereum) {
                alert('No Wallet found.');
                return;
            }

            window.ethereum.request({
                method: 'wallet_addEthereumChain',
                params: [{
                    "chainId": "0x64",
                    "chainName": "xDai",
                    "rpcUrls": ["https://rpc.xdaichain.com"],
                    "nativeCurrency": {
                        "name": "xDai Chain xDai",
                        "symbol": "xDai",
                        "decimals": 18,
                    },
                    "blockExplorerUrls": ["https://blockscout.com/poa/xdai"]
                }, ],
                id: 1,
            }, console.log);

            window.ethereum.request({
                method: 'wallet_watchAsset',
                params: {
                    type: 'ERC20',
                    options: {
                        address: '0x63e62989d9eb2d37dfdb1f93a22f063635b07d51',
                        symbol: 'MIVA',
                        decimals: 18,
                        image: 'https://dev.lab10.io/minerva/MIVA_Logo.svg',
                    }
                },
            }, console.log);
        });

</script>

{% endfor %}
