## Web Integration

Integrate Moru Checkout into your website.

## Prerequisite

Following things will be required before you can begin integration:

- Moru gateway user account
- Access & Secret Key

Moru Checkout can be integrate into your website using pure JavaScript or using ES modules (in React.Js)

## Integration Steps for Pure Javascript

1. Include moru checkout.Js in your HTML head

```html
<head>
  <script src="https://web.payment-gateway.moru.com.np/sdk/build/moru-checkout.js"></script>
</head>
```

2. Add below code to js script

The given below is the Sample JS Code to initialize the payment -

```html
<script>
  const options = {
    access_key: 'test_9425294388834bdface7d1b58fd538bf67627d9408fe4f2589820cf550a5003d',
    transaction_id: '1',
    additional_fields: {
      name: 'Firstname Lastname',
      email: 'email@example.com',
    },
    callback_handler: {
      onSuccess: (response) => {
        console.log(response);
        // call your api
        alert('success');
      },
      onError: (error) => {
        console.log(error);
        alert('failure');
      },
      onClose: (error) => {
        console.log(error);
      },
    },
  };
  const checkout = new MoruCheckout(options);
  const handleMoruPayment = () => {
    checkout.open({ amount: 100 });
  };
</script>
```

3. Pay Button

Place this button in your HTML code, so a user can click on it and proceed to pay.

```html
<button onclick="handleMoruPayment()">Pay with Moru</button>
```

## Sample Code

```html
<html>
  <head>
    <script src="https://web.payment-gateway.moru.com.np/sdk/build/moru-checkout.js"></script>
  </head>
  <body>
    <button onclick="handleMoruPayment()">Pay with Moru</button>
    <script>
      const options = {
        access_key: 'test_9425294388834bdface7d1b58fd538bf67627d9408fe4f2589820cf550a5003d',
        transaction_id: '1',
        additional_fields: {
          name: 'Firstnname Lastname',
          email: 'email@example.com',
        },
        callback_handler: {
          onSuccess: (response) => {
            console.log(response);
            // call your api
            alert('success');
          },
          onError: (error) => {
            console.log(error);
            alert('failure');
          },
          onClose: (error) => {
            console.log(error);
          },
        },
      };
      const checkout = new MoruCheckout(options);
      const handleMoruPayment = () => {
        checkout.open({ amount: 100 });
      };
    </script>
  </body>
</html>
```

## Integration Steps for ES Modules

### Installation

#### USING YARN

```bash
yarn add @moruwallet/moru-web-sdk
```

#### USING NPM

```bash
npm install @moruwallet/moru-web-sdk
```

#### Usage in React.Js

```jsx
import { MoruCheckout } from '@moruwallet/moru-web-sdk';

function App() {
  const options = {
    access_key: 'test_9425294388834bdface7d1b58fd538bf67627d9408fe4f2589820cf550a5003d',
    transaction_id: '1',
    additional_fields: {
      name: 'Firstnname Lastname',
      email: 'email@example.com',
    },
    callback_handler: {
      onSuccess: (response) => {
        console.log(response);
        // call your api
        alert('success');
      },
      onError: (error) => {
        console.log(error);
        alert('failure');
      },
      onClose: (error) => {
        console.log(error);
      },
    },
  };
  const checkout = new MoruCheckout(options);
  const handleMoruPayment = () => {
    checkout.open({ amount: 100 });
  };
  return (
    <div>
      <button onClick={handleMoruPayment}>Pay with Moru</button>
    </div>
  );
}

export default App;
```

## API

- MoruCheckout(options)

  - instantiate MoruCheckout class with given set of options (option is a javascript object )

- open(options?)

  - Open is a method to open the Morucheckout UI in your website. It task the options as an argument.

### Options is a Javascript object with -

| Properties        | Required | Type     | value                                                                    |
| ----------------- | -------- | -------- | ------------------------------------------------------------------------ |
| access_key        | True     | `string` | Test or live access key                                                  |
| transaction_id    | True     | `string` | Unique `transaction id` used to verify the payment status of transaction |
| additional_fields | False    | `object` | Additional data of the transaction                                       |
| callback_handler  | True     | `object` | Javascript object to handle the success and failure events               |
| amount            | True     | `string` | Amount to pay                                                            |

- callback_handler

callback_handler has three methods onSuccess, onError and onClose

- onSuccess(response)

  when transaction is completed successfully, onSuccess event will trigger with the success response

```js
{
  amount: 100,
  moru_txn_identifier: '58967f7d2e39496e94d61a8f07488245',
  status: 'success',
  stausCode: 200,
}
```

> After transaction is completed in client page, you need to do the server side verification about the status of the transaction
