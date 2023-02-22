<html>

<body>
<h1 align = "center">AWS-LAMBDA-AND-SERVERLESS-FRAMEWORK</h1>

<pre>Deploy your initial <a href="https://www.serverless.com/aws-lambda">AWS Lambda</a> Function as an API Gateway endpoint by leveraging the power of the Serverless Framework </pre>
  <h2>What is Serveless ?</h2>
  <p>Serverless Framework is <em>open source</em> software that builds, compiles, and packages code for serverless deployment, and then deploys the package to the    cloud</p>
  <p>The term itself might be a little bit confusing as it indicates that there are no servers being used which is not true. There are servers involved however you as a developer don't have to worry about how your code is going to be executed, all the server management is going to be handled by the provider company (AWS in our case).</p>
  
<br>
<h2>Prerequisites</h2>
<ol>
<li>
<a href = "https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/">Create and activate a new AWS account</a>
</li>

<li>
<a href = "https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html">Create an IAM user</a>
</li>
<li>
<a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html">Install AWS CLI </a>
</li>
<li>
<a href = "https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-config">AWS configuration</a>
</li>
&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; You'll need  <em> AWS Access Key ID</em> and <em>Secret Key</em> for AWS CLI configuration. </mark>
<li>
<a href = "https://nodejs.org/en/">Install latest Node.js</a>
</li>
</ol>
<h2>Setting Up Serverless Framework With AWS</h2>
<h3>Step 1. Install serverless framework globally with npm</h3>
<pre>npm install -g serverless</pre>

<h3>Step 2. Create serverless project from the template</h3>

<p>a. Create a new directory and change it to where you would like your new serverless project to be created, for example:</p>
<pre>cd ~/Projects</pre>

<p>b. To create a new serverless project from the default template run:</p>
<pre>serverless create --template aws-nodejs --path my-lambda-function</pre>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Here "my-lambda-function" is the name of the folder where your project is going to be created.</p>

<p>c. Open a newly created project (my-lambda-function folder) with a code editor now(vs-code,sublime,etc.)</p>
<p>d. Open serverless.yml file.</p>

<h3>Step 3. serverless.yml</h3>
<p>The serverless.yml file stores all of our lambda configuration, here is how it's going to look like (I removed all the commented out code that are irrelevant).<br><br>
This is how your serverless.yml file should look like: 
<a href = "https://github.com/devpeak/AWS-LAMBDA-AND-SERVERLESS-FRAMEWORK/blob/master/my-lambda-function/serverless.yml">serverless.yml</a></p>


<h3>Step 4. handler.js</h3>

<p>Lambda function code is located in handler.js <br>
Default content of this file should be as follows:</p>
<pre>'use strict';

module.exports.hello = async (event) => {
  return {
    statusCode: 200,
    body: JSON.stringify(
      {
        message: 'Go Serverless v1.0! Your function executed successfully!',
        input: event,
      },
      null,
      2
    ),
  };

  // ...
};
</pre>
<ul>
<li><em>module.exports.hello</em> with hello being the name of the function</li>
<li><em>event</em> argument containing all the request information - params, headers, body and extra info from API Gateway </li>
<li><strong>return</strong> object with required statusCode and body properties - this is going to be the returned response</li>
</ul>
<p>There is no need to make any changes in the file, Althrough I'm going to change the message and add one more property to the response body:</p>
<pre>'use strict';

module.exports.hello = async (event) => {
  return {
    statusCode: 200,
    body: JSON.stringify(
      {
        // changed message
        message: 'Hello from AWS Lambda!',
        // added statusCode
        statusCode: 200,
        input: event,
      },
      null,
      2
    ),
  };

  // ...
};
</pre>

<h3>Step 5. Let's Deploy</h3>
In the terminal run the following command from projects\my-lambda-function directory.
<pre>serverless deploy</pre>
<p>If your AWS CLI is configured correctly, after few minutes of waiting you should see the success message and URL to your newly created endpoint</p>
 <pre>(node:8908) NOTE: The AWS SDK for JavaScript (v2) will be put into maintenance mode in 2023.

Please migrate your code to use AWS SDK for JavaScript (v3).
For more information, check the migration guide at https://a.co/7PzMCcy
(Use `node --trace-warnings ...` to show where the warning was created)

Deploying my-lambda-function to stage dev (us-east-1)

✔ Service deployed to stack my-lambda-function-dev (158s)

endpoint: GET - https://5vzwbdagil.execute-api.us-east-1.amazonaws.com/dev/hello
functions:
  hello: my-lambda-function-dev-hello (411 B)</pre>
  
  <h4>Endpoints</h4>
  <pre>The endpoint is located here: https://5vzwbdagil.execute-api.us-east-1.amazonaws.com/dev/hello </pre>

<h3>Step 6. Testing</h3>
<p>To check if your endpoint works correctly simply copy and paste the API Gateway endpoint URL to your browser:</p>
<img src = "https://user-images.githubusercontent.com/100518568/220396569-478f99e4-80c1-4608-a6bd-279d9d0fd625.png">

<br><br><br>
<h1 align ="center">CONGRATS!!! You successfully created and deployed an AWS Lambda Function as an API Gateway Endpoint!</h1>
</body>


</html>

