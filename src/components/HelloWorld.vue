<template>
<div class="min-h-screen bg-gray-900">
  <div class="relative overflow-hidden">
    <header class="relative">
      <div class="bg-gray-900 pt-6">
        <nav class="relative max-w-7xl mx-auto flex items-center justify-between px-4 sm:px-6" aria-label="Global">
          <div class="flex items-center flex-1">
          </div>
          <div class="md:space-x-6">
            <a href="https://github.com/ensconce/crowatch" class="inline-flex items-center px-4 py-2 border border-transparent text-base font-medium rounded-md text-white bg-gray-600 hover:bg-gray-700">
              <svg class="h-6 w-6 mr-2" viewBox="0 0 16 16" fill="currentColor"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"></path></svg>
              Grab source
            </a>
          </div>
        </nav>
      </div>
    </header>

    <main>
      <div class="pt-10 bg-gray-900 sm:pt-16 lg:pt-8 lg:pb-14 lg:overflow-hidden">
        <div class="mx-auto max-w-7xl lg:px-8">
          <div class="lg:grid lg:grid-cols-2 lg:gap-8">
            <div class="mx-auto max-w-md px-4 sm:max-w-2xl sm:px-6 sm:text-center lg:px-0 lg:text-left lg:flex lg:items-center">
              <div class="lg:py-24">
                <h1 class="mt-4 text-4xl tracking-tight font-extrabold text-white sm:mt-5 sm:text-6xl lg:mt-6 xl:text-6xl">
                  <span class="block">Count your CRO</span>
                  <span class="block text-indigo-400">{{state.totalRewards.toFixed(2)}} CRO</span>
                </h1>
                <p class="mt-3 text-base text-gray-300 sm:mt-5 sm:text-xl lg:text-lg xl:text-xl">
                  Since it's hard to count crows I tried making it a bit simpler.
                  Add multiple wallet addresses to watch, nothing gets saved to our servers, everything is kept locally on your computer.
                </p>
                <div class="mt-10 sm:mt-12">
                  <form action="#" class="sm:max-w-xl sm:mx-auto lg:mx-0">
                    <div class="sm:flex">
                      <div class="min-w-0 flex-1">
                        <label for="text" class="sr-only">Enter your wallet address</label>
                        <input id="text" v-model="state.address" type="text" placeholder="Enter wallet address" class="block w-full px-4 py-3 rounded-md border-0 text-base text-gray-900 placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-300 focus:ring-offset-gray-900">
                      </div>
                      <div class="mt-3 sm:mt-0 sm:ml-3">
                        <button type="button" @click="saveAddress()" class="block w-full py-3 px-4 rounded-md shadow bg-indigo-500 text-white font-medium hover:bg-indigo-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-300 focus:ring-offset-gray-900">Start monitoring</button>
                      </div>
                    </div>
                    <p class="mt-3 text-sm text-gray-300 sm:mt-4">This tool may or may not give you an accurate view of your total earnings, use at your own risk. This tool nor it's creator is affiliated with Crypto.com in any way.</p>
                  </form>
                </div>
              </div>
            </div>
            <div class="mt-12 -mb-16 sm:-mb-48 lg:m-0 lg:relative hidden lg:inline-flex">
              <div class="mx-auto max-w-md px-4 sm:max-w-2xl sm:px-6 lg:max-w-none lg:px-0">
                <img class="w-full lg:absolute lg:inset-y-0 lg:left-0 lg:h-full lg:w-auto lg:max-w-none " src="/undraw_Stock_prices_re_js33.svg" alt="">
              </div>
            </div>
          </div>
          <div class="flex flex-col mt-20">
            <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
              <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
                <div class="shadow overflow-hidden border-b border-gray-600 sm:rounded-lg">
                  <table class="min-w-full divide-y divide-gray-600">
                    <thead class="bg-gray-800">
                      <tr>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                          Wallet
                        </th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                          Balance
                        </th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                          Claimed
                        </th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                          Unclaimed
                        </th>
                        <th scope="col" class="relative px-6 py-3">
                          <span class="sr-only">Remove</span>
                        </th>
                      </tr>
                    </thead>
                    <tbody class="bg-gray-800 divide-y divide-gray-600">
                      <template v-for="address in state.addresses" v-bind:key="address.address">
                      <tr>
                        <td class="px-6 py-4 whitespace-nowrap">
                          <div class="flex items-center">
                            <div class="flex-shrink-0 h-10 w-10">
                              <img src="https://assets.coingecko.com/coins/images/7310/large/cypto.png" class="h-10 w-10">
                            </div>
                            <div class="ml-4">
                              <div class="text-sm font-medium text-white">
                                <a v-bind:href="'https://crypto.org/explorer/account/'+address.address" target="_blank">{{address.address}}</a>
                              </div>
                            </div>
                          </div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                          <div class="text-sm text-white">{{address.balance}} CRO</div>
                          <div class="text-sm text-gray-500">${{ (address.balance * state.CROPrice).toFixed(2) }} USD</div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                          <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">
                            {{address.rewards}} CRO
                          </span>
                          <div class="text-sm text-gray-500">${{ (address.rewards * state.CROPrice).toFixed(2) }} USD</div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                          <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">
                            {{address.active}} CRO
                          </span>
                          <div class="text-sm text-gray-500">${{ (address.active * state.CROPrice).toFixed(2) }} USD</div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                          <button @click="removeAddress(address.address)" class="text-indigo-600 hover:text-indigo-900">
                            
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                            </svg>

                          </button>
                        </td>
                      </tr>
                      </template>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>



          <template v-for="address in state.addresses" v-bind:key="address.address">
          <div class="flex flex-col mt-20">
            <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
              <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
                <div class="shadow overflow-hidden border-b border-gray-600 sm:rounded-lg">
                  <table class="min-w-full divide-y divide-gray-600">
                    <thead class="bg-gray-800">
                      <tr>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                          Transaction
                        </th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                          Reward
                        </th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                          Claimed at
                        </th>
                      </tr>
                    </thead>
                    <tbody class="bg-gray-800 divide-y divide-gray-600">
                      <template v-for="transaction in address.transactions" v-bind:key="transaction.hash">
                      <tr>
                        <td class="px-6 py-4 whitespace-nowrap">
                          <div class="flex items-center">
                            <div class="flex-shrink-0 h-10 w-10">
                              <img src="https://assets.coingecko.com/coins/images/7310/large/cypto.png" class="h-10 w-10">
                            </div>
                            <div class="ml-4">
                              <div class="text-sm font-medium text-white">
                                <a v-bind:href="'https://crypto.org/explorer/tx/'+transaction.hash" target="_blank">{{transaction.hash}}</a>
                              </div>
                            </div>
                          </div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                          <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">
                            {{ ( transaction.messages[0].content.amount[0].amount / 100000000) }} CRO
                          </span>
                          <div class="text-sm text-gray-500">${{ (( transaction.messages[0].content.amount[0].amount / 100000000) * state.CROPrice).toFixed(2) }} USD</div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                          <div class="text-sm font-medium text-white">
                            {{transaction.blockTime}}
                          </div>
                        </td>
                      </tr>
                      </template>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>
        </template>


        </div>
      </div>
    </main>
  </div>
  <div class="fixed inset-x-0 bottom-0">
    <div class="bg-gray-800">
      <div class="max-w-7xl mx-auto py-3 px-3 sm:px-6 lg:px-8">
        <p class="ml-3 font-medium text-white truncate text-center">
          Buy me a beer 
          <svg  xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white inline" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          cro1u4drqzsd30ta9vgjn3lzxfk8t2rtcdjzkp2gcj
        </p>
      </div>
    </div>
  </div>
</div>
</template>

<script setup>
import { defineProps, reactive } from 'vue'
import axios from 'axios'

const state = reactive({
  address: "",
  addresses: [],
  totalRewards: 0,
  totalRewardsUsd: 0,
  activeReward: 0,
  CROPrice: 0,
});


const saveAddress = () => {
  state.addresses.push( { address: state.address, rewards: 0, active: 0, balance: 0, transactions: [], page: 1, limit: 20, lastHeight: 0 } );
  fetchWallet();
  state.address = "";
  localStorage.setItem("addresses", JSON.stringify(state.addresses));
}

const removeAddress = (_addr) => {
  state.addresses.forEach(function (address, index) {
    if(address.address == _addr) {
      state.addresses.splice(index, 1);
      localStorage.setItem("addresses", JSON.stringify(state.addresses));
    }
  });
  state.totalRewards = 0;
  state.activeReward = 0;
  state.addresses.forEach(function (address, index) {
    state.rewards = 0;
    state.active = 0;
    state.balance = 0;
  });
}

const fetchTokenPrice = (vs) => {
  axios.get(`https://api.coingecko.com/api/v3/simple/price?ids=crypto-com-chain&vs_currencies=usd`)
    .then(function (response) {
      state.CROPrice = response.data['crypto-com-chain'].usd;
    })
    .catch(function (error) {
      // handle error
      console.log(error);
    })
    .then(function () {
      // always executed
    })
}

const fetchTransactionsRecursive = (address, index) => {
  //state.addresses.forEach(function (address, index) {
    console.log(`https://crypto.org/explorer/api/v1/accounts/${address.address}/transactions?pagination=offset&page=${address.page}&limit=${address.limit}&order=height.asc`);
    axios.get(`https://crypto.org/explorer/api/v1/accounts/${address.address}/transactions?pagination=offset&page=${address.page}&limit=${address.limit}&order=height.asc`)
    .then(function (response) {
      state.addresses[index].transactions.push(response.data.result);
      localStorage.setItem("addresses", JSON.stringify(state.addresses));
      if(response.data.pagination.total_page > response.data.pagination.current_page) {
        state.addresses[index].page++;
        fetchTransactionsRecursive(address, index);
      }
    })
    .catch(function (error) {
      // handle error
      console.log(error);
    })
    .then(function () {
      // always executed
    })
  //})
}


const fetchTransactions = () => {
  state.addresses.forEach(function (address, index) {
    axios.get(`https://crypto.org/explorer/api/v1/accounts/${address.address}/transactions?pagination=offset&page=1&limit=1000&order=height.asc`)
    .then(function (response) {

      if(index == 0) {
        state.totalRewards = 0;
      }

      let rewards = 0;
      state.addresses[index].transactions = [];
      response.data.result.forEach(transaction => {
        if(transaction.messages[0].content.name == "MsgWithdrawDelegatorRewardCreated") {
          state.addresses[index].transactions.push(transaction);
          rewards += Math.round( (parseFloat(transaction.messages[0].content.amount[0].amount) / 100000000) * 100,2) / 100; 
        }
      });

      state.addresses[index].rewards = Math.round(rewards * 100,2) / 100;
      state.totalRewards += Math.round( (rewards + state.activeReward) * 100,2) / 100;

      console.log(state.totalRewards);
    })
    .catch(function (error) {
      // handle error
      console.log(error);
    })
    .then(function () {
      // always executed
    })
  })
}

const fetchWallet = () => {
  
  state.addresses.forEach(function (address, index) {
    axios.get(`https://crypto.org/explorer/api/v1/accounts/${address.address}`)
    .then(function (response) {
      // handle success
      if(index == 0) {
        state.activeReward = 0;
      }
      let sum = 0;
      let balance = 0;

      response.data.result.totalRewards.forEach(reward => {
        sum += Math.round( (parseFloat(reward.amount) / 100000000) * 100,2) / 100;
      });

      response.data.result.totalBalance.forEach(totalBalance => {
        balance += Math.round((parseFloat(totalBalance.amount)  / 100000000) * 100,2) / 100;
        console.log(balance);
      });

      state.addresses[index].active = sum;
      state.addresses[index].balance = balance;
      state.activeReward += sum;
    })
    .catch(function (error) {
      // handle error
      console.log(error);
    })
    .then(function () {
      // always executed
    });
    //console.log("FETCH RECURSIVE!");
    //fetchTransactionsRecursive(address, index);
  });
  fetchTransactions();
}

if(localStorage.getItem("addresses") !== null) {
  state.addresses = JSON.parse(localStorage.getItem("addresses"));
  fetchWallet();
}
fetchTokenPrice();

  setInterval(() => {
    fetchWallet()
  }, 10000);

</script>
