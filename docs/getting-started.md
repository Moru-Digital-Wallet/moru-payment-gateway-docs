## Before you begin your integration

You should have applied for moru payment gateway user and have received your test access key & secret key. If you haven’t registered with moru yet, please sign up at app.moru.com.np. If you need any help while creating an account feel free to contact us.
After receiving the test credentials you can now follow this document instruction on integrating sdk on your web or mobile application.

## Integration Flow

The full integration completes in two steps:

1. First you need to integrate in the client side. The client web and mobile application have the sdk to be integrated. The client sdk will creates a layout for users to login and proceed payment. Once the payment is done by the user, the sdk sends response to the client page.

2. Second steps is to setup the API call from your server. To verify the transaction that was completed from client page, you need to call the transaction verification api from your server. The verification api sends the transaction status as a response.

## During the integration

You will be provided with the test credentials (access key and secret key) once registered as a moru gateway user. The test keys will be used during the integration process.

During the course of your integration, we would be happy to assist you in any way possible, please reach out to us on contact@moru.com.np with your query.

## Moving to production

After you have completed and tested your integration, please reach out to our team (contact@moru.com.np) and we will review your integration and help you get ready to go on production. After we have checked your integration, and all other processes for onboarding you on to our payment partners have been completed, you will be able to see your Live environment access key & secret key. You will need to change to these keys to link to the Live environment.
