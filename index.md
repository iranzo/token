---
title: Add token/network definitions to Metamask
tags: [metamask, wallet]
---

## Networks

{% for item in site.data.networks %}
{% assign network = item[1] %}

<div class="buttonWrapper">
    <button class="add{{ network.name }}" type="button">Add Network
            <span>${{ network.name }}</span> to your
            <span>wallet</span>
    </button>
</div>
<script>
document.querySelector('.add{{ network.name }}').addEventListener('click', (e) => {
    e.preventDefault();
    if (!window.ethereum) {
        alert('No Wallet found.');
        return;
    }

    window.ethereum.request({
        method: 'wallet_addEthereumChain',
        params: [{
            "chainId": "{{ network.ID }}",
            "chainName": "{{ network.name }}",
            "rpcUrls": ["{{ network.RPCURL }}"],
            "nativeCurrency": {
                "name": "{{ network.name }} Chain {{ network.Symbol }}",
                "symbol": "{{ network.Symbol }}",
                "decimals": 18,
            },
            "blockExplorerUrls": ["{{ network.blockexplorer }}"]
        }, ],
        id: 1,
    }, console.log);

});
</script>

{% endfor %}

## Tokens

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
