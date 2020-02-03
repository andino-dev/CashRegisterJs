# CashRegisterJs
JavaScript Algorithms and Data Structures Projects: Cash Register Design a cash register drawer function checkCashRegister() that accepts purchase price as the first argument (price), payment as the second argument (cash), and cash-in-drawer (cid) as the third argument.  cid is a 2D array listing available currency.  The checkCashRegister() function should always return an object with a status key and a change key.  Return {status: "INSUFFICIENT_FUNDS", change: []} if cash-in-drawer is less than the change due, or if you cannot return the exact change.  Return {status: "CLOSED", change: [...]} with cash-in-drawer as the value for the key change if it is equal to the change due.  Otherwise, return {status: "OPEN", change: [...]}, with the change due in coins and bills, sorted in highest to lowest order, as the value of the change key.
```javascript

 var denom = [
  { name: 'ONE HUNDRED', val: 100.00},
  { name: 'TWENTY', val: 20.00},
  { name: 'TEN', val: 10.00},
  { name: 'FIVE', val: 5.00},
  { name: 'ONE', val: 1.00},
  { name: 'QUARTER', val: 0.25},
  { name: 'DIME', val: 0.10},
  { name: 'NICKEL', val: 0.05},
  { name: 'PENNY', val: 0.01}
];
function checkCashRegister(price, cash, cid) {
  var change = cash-price;
  var response = {status:null,change:[]};
  var cidA = cid.reduce(function(acc, curr) {
    acc.total += curr[1];
    acc[curr[0]] = curr[1];
    return acc;
  }, { total: 0 });

  if(cidA.total===change){
    response.status ="CLOSED";
    response.change = cid;
    return response;
  } if (cidA.total < change) {
    response.status = 'INSUFFICIENT_FUNDS';
    return response;
  }
  var change_arr = denom.reduce(function(acc, curr) {
    var value = 0;
     while (cidA[curr.name] > 0 && change >= curr.val) {
      change -= curr.val;
      cidA[curr.name] -= curr.val;
      value += curr.val;
       change = Math.round(change * 100) / 100;
    }
     if (value > 0) {
        acc.push([ curr.name, value ]);
    }
    return acc;
    }, []);
    if (change_arr.length < 1 || change > 0) {
    response.status = 'INSUFFICIENT_FUNDS';
    return response;
  }
response.status = 'OPEN';
  response.change = change_arr;
  return response;
  
  // Here is your change, ma'am.

}

// Example cash-in-drawer array:
// [["PENNY", 1.01],
// ["NICKEL", 2.05],
// ["DIME", 3.1],
// ["QUARTER", 4.25],
// ["ONE", 90],
// ["FIVE", 55],
// ["TEN", 20],
// ["TWENTY", 60],
// ["ONE HUNDRED", 100]]

console.log(checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]));

```
