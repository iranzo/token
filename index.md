---
title: Add tokens to Metamask
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
                        address: '{{ token.contract }}',
                        symbol: '{{ token.name }}',
                        decimals: 18,
                        image: '{{ token.image}}',
                    }
                },
            }, console.log);
        });

</script>

{% endfor %}
