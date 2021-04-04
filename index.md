---
title: Add network definitions to Metamask
tags: [metamask, wallet]
---

## Networks

{% for item in site.data.networks %}
{% assign network = item[1] %}
{% for item in site.data.tokens %}
{% assign token = item[1] %}
{% if token.network == network.friendly  %}

<div class="buttonWrapper">
<img src='{{token.image}}' height=32 widht=32>
    <button class="add{{token.name}}" type="button">Add
            <span>${{ token.name }}</span> to your
            <span>wallet</span> on network {{ network.friendly }}
    </button>
</div>

<script>
document.querySelector('.add{{ token.name }}').addEventListener('click', (e) => {
    e.preventDefault();
    if (!window.ethereum) {
        alert('No Wallet found.');
        return;
    };

{% if network.friendly != "Ethereum" %}

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

{% endif %}

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

{% endif %}
{% endfor %}

{% endfor %}
