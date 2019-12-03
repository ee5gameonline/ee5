
Instantiation  scatter
Nodejs
import ScatterJS from '@scatterjs/core';
import ScatterEOS from '@scatterjs/eosjs'

ScatterJS.plugins( new ScatterEOS() );
Vanilla
<script src="scatterjs-core.min.js"></script>
<script src="scatterjs-plugin-eosjs.min.js"></script>

<script>
    ScatterJS.plugins( new ScatterEOS() );
</script>
Multiple Plugins
import ScatterJS from '@scatterjs/core';
import ScatterEOS from '@scatterjs/eosjs'
import ScatterTron from '@scatterjs/tron'
import ScatterLynx from 'scatterjs-plugin-lynx'

ScatterJS.plugins( new ScatterEOS(), new ScatterTron(), new ScatterLynx(Eos || {Api, JsonRpc}) );



Build the network object
Networks tell Scatter which blockchain nodes you're going to be working with.

const network = ScatterJS.Network.fromJson({
    blockchain:'eos',
    chainId:'aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906',
    host:'nodes.get-scatter.com',
    port:443,
    protocol:'https'
});



Connect to an available wallet
Once you are connected you can then call API methods on ScatterJS

ScatterJS.connect('MyAppName', {network}).then(connected => {
    if(!connected) return false;
    // ScatterJS.someMethod();
});

Getting Blockchain Accounts
Login with the network passed into ScatterJS.connect

ScatterJS.login().then(...);
Login with multiple networks

ScatterJS.login({accounts:[network1, network2]).then(...);
Logout

ScatterJS.logout().then(...);
After a successful login, the "Identity" will be available at ScatterJS.identity. If a user refreshes the page and has already logged in, the ScatterJS.identity property will be auto-filled.




Get blockchain accounts from the identity
Because accounts are nested within the Identity there is an easy method for fetching them.

Using the helper
const account = ScatterJS.account('eos')
// Result: {name:'...', authority:'active', publicKey:'...', blockchain:'eos', chainId:'...'}

const account = ScatterJS.account('eth')
// Result: {address:'...', blockchain:'eth', chainId:'1'}

const account = ScatterJS.account('trx')
// Result: {address:'...', blockchain:'trx', chainId:'1'}


From the Identity
const account = ScatterJS.identity.accounts.find(x => {
    return x.blockchain === 'eos';
});
