---
title: Add network definitions to Metamask
tags: [metamask, wallet]
---

## Networks

{% for item in site.data.networks %}
{% assign network = item[1] %}

<div class="buttonWrapper">
    <button class="add{{ network.Symbol }}" type="button">Add Network
            <span>${{ network.name }}</span> to your
            <span>wallet</span>
    </button>
</div>
<script>
document.querySelector('.add{{ network.Symbol }}').addEventListener('click', (e) => {
    e.preventDefault();
    if (!window.ethereum) {
        alert('No Wallet found.');
        return;
    };

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
