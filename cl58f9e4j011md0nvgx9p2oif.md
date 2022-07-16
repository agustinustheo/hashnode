## How To Write Clean API Calls With Axios

Making front-end applications is not as simple as it used to be. Frontend frameworks like React and Vue.js rely heavily on APIs. This adds complexity to our app because we need to manage how we call these APIs. One solution is to simplify the process by writing clean API calls.

But wait, what are “clean API calls”? To me, that means the proper structuring of API calls, making them easy to read and maintain. First, I do this by utilizing the single-responsibility principle. Each function must have a single responsibility, and with this principle in mind, we need to separate the logic for each endpoint.

The other thing I try to consider is the DRY principle (“Don’t Repeat Yourself”). This is very important — arguably more so in the case of frontend API providers — because it gives a sense of tidiness in the code, thus improving readability. I use [Axios](https://www.npmjs.com/package/axios) because it gives features such as interceptors, defaults, etc. It reduces the amount of boilerplate code you need to write for each API endpoint.

### Pros and Cons of Using Axios

There are many ways to achieve this. You can either use the Fetch API or you can use a third-party library called Axios. By the title of this article, you can guess that I prefer Axios. Why? Let’s weigh in on the pros and cons.

#### **Pro: Simplicity**

What I like most about Axios is that it is very simple to use. The programming API is so easy to use that I have gotten really used to it. Well, this might be too personal of a preference, but you can try it yourself. I have used jQuery’s AJAX and the Fetch API, and I would rank Axios above all of them — although not by too large of a margin since all three of them are nice to work with.

#### **Pro: Backward compatibility**

Honesty, you wouldn’t think about this feature until you needed it. I mean, most people have modern browsers, but if some of your customers aren’t most people, they might not be able to use your app if it isn’t backward-compatible. The Fetch API is relatively new and old browsers aren’t capable of using it. Otherwise, libraries like Axios and jQuery’s AJAX are built on top of JavaScript’s XMLHttpRequest. For those of you who are wondering, XMLHttpRequest is an old version of JavaScript’s built-in HTTP calling mechanism.

#### **Pro: Mature library with lots of features**

You can do a lot with Axios — a whole lot. For example, as of the writing of this article, the Fetch API does not have built-in request/response interceptors. You have to use third parties. Compared to Fetch, writing clean APIs using Axios is very simple. Axios already has so many built-in conveniences. To name a few, you can set default headers and default base URLs using Axios.

#### **Con: Too sophisticated for small apps**

I have used Axios for long enough to understand that this library can be *overkill* for small apps. If you only need to use its GET and POST-APIs, you probably are better off with the Fetch API anyway. Fetch is native to JavaScript, whereas Axios is not. This brings us to the next point.

#### **Con: Axios bloats your bundle size**

This second point corresponds to the first one perfectly. One of the main reasons I avoid the use of Axios for small apps is the fact that it bloats your production build size. Sure, you might not notice a size spike for large apps like in e-commerce and such. But you will notice a huge increase if you are making a simple portfolio site. The lesson to be learned? Use the right tools for the right job.

#### **Con: It’s a third party**

Look, let me just start by saying that this third point is really subjective and some people might have opposite views. Axios is a third party. Yes, you read that right. Unlike Fetch, it is not native to the browser. You are depending on the community to maintain your precious app. Then again, most apps these days do use open-source products. So would it be a problem? Not really. Again, this is a preference. I am not advising you to reinvent the wheel. Just understand that you don’t *own* the wheel.

### Installing Axios

Axios is available in multiple JavaScript repositories. You can access it using yarn and NPM. If you are using regular HTML, you can import it from CDNs like jsDelivr, Unpkg, or Cloudflare.

Assuming you are using NPM, we need to install Axios using this command:

npm install -S axios

If there are no errors in the installation, you can continue to the next step. You can check alternative installation methods [on GitHub](https://github.com/axios/axios#installing).

### Making Separate Axios Clients

What are Axios clients? Clients are how we set default parameters for each API call. We set our default values in the Axios clients, then we export the client using JavaScript’s `export default`. Afterward, we can just reference the client from the rest of our app.

First, make a new file preferably named `apiClient.js` and import Axios:

Import Axios.

Then make a client using `axios.create`:

Axios client JS example.

As you can see, we initiated the base URLs and default headers for all our HTTP calls.

### Using Interceptors for Clean Redirects

When calling interacting APIs — especially when there is authentication involved — you will need to define conditions when your call is unauthorized and make your application react appropriately. Interceptors are perfect for this use case.

Let’s say that we need our application to redirect us to our home page when our cookies expire, and when our cookies expire, the API will return a 401 status code. This is how you would go about it:

Example of using Axios interceptors.

Simple, right? After you’ve defined your client and attached an interceptor, you just need to export your client to be used on other pages.

### Exporting Axios Client

After configuring your Axios client, you need to export it to make it available for the entire project. You can do this by using the `export default` feature:

Export Axios Client.

Now we have made our Axios client available for the entire project. Next, we will be making API handlers for each endpoint.

### Folder Structure

Before we continue, I thought it would be useful to show you how to arrange your subfolders. Instead of writing a long comprehensive explanation, I think it would be better for me to give you an image of what I am talking about:

![Folder structure](https://cdn.hashnode.com/res/hashnode/image/upload/v1657037406213/-QMEn6Gte.png)

How I would arrange my folders.

This assumes we will have admin, user, and product endpoints. We will home the `apiClient.js` file inside the root of the network folder. The naming of the folder or even the structure is just my personal preference.

The endpoints will be put inside a `lib` folder and separated by concerns in each file. For example, for authentication purposes, user endpoints would be put inside the user file. Product-related endpoints would be put inside the product file.

### Writing an API Handler

Now we will be writing the API handler. Each endpoint will have its asynchronous function with custom parameters. All endpoints will use the client we defined earlier. In the example below, I will write two API handlers to get new products and add new products:

Example of product endpoint provider.

This pretty much sums up how I would write an API handler, and as you can see, each API call is clean and it all applies the single-responsibility principle. You can now reference these handlers on your main page.

### Using the Handlers in Your Web App

Assuming that you are using an NPM project for all of this, you can easily reference your JavaScript API handlers using the `import` method. In this case, I will be using the `getProduct` endpoint:

Use get product endpoint.

There you have it: a clean no-fuss API handler. You’ve successfully made your app much more readable and easier to maintain.

### Final Words

Having an app that works is great. You got all the functionalities right and you are practically finished. However, people tend to forget that they need to maintain that app. So, sooner or later, you will have to read that code all over again. And wouldn’t it be better if it was all readable and easy to understand with great separation of concerns? I think we would all want that, and I would even say we would be very proud if we could read the code we wrote one year ago.

Being fast does not guarantee success, but being consistent and responsible does. Write better code and help your team grow! Thanks for reading.

*Originally published at* [*https://daily.dev*](https://daily.dev/blog/a-guide-to-writing-clean-api-calls-using-axios) *on March 9, 2021.*

*Edit Note: I made a mistake and said the Fetch API is native to Javascript while actually,* [*it is not, it is native to the browser*](https://stackoverflow.com/questions/44058726/is-the-fetch-api-an-ecmascript-feature)*, and old browsers do not support it. You can read about it more* [*here*](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)*. Thanks for the comment* [*Nick Howard*](https://medium.com/u/52e936b1a62b)*!*