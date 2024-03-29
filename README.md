# OpenTelemetry Sample: Django simple API instrumented with OTEL and Digma

This repository contains a sample application used to test various scenarios, performance bottlenecks and runtime errors with [Digma](https://github.com/digma-ai/digma). This sample uses the standard OTEL instrumentation library as well as the [Digma instrumentation for Python](https://github.com/digma-ai/opentelemetry-instrumentation-digma) and [Digma instrumentation for Django](https://github.com/digma-ai/opentelemetry-instrumentation-digma-django) helper packages.

Note that this app requires an operational Digma backend. If you haven't already set up the backend, follow our [simple instructions](https://github.com/digma-ai/digma) to get it up and running quickly.

## Prerequisites
- [Python 3.8+](https://www.python.org/downloads/)
- [VS Code](https://code.visualstudio.com/download)

## Running the app with Digma

### Install the IDE extension

1. Install the [Digma Extension](https://marketplace.visualstudio.com/items?itemName=digma.digma) in the vsCode IDE.
2. Open the 'Settings' tab of the extension.

![image](https://user-images.githubusercontent.com/93863/165008075-96fa40cd-a566-4c69-9481-195f69f3c425.png)

3. Set the 'Digma URL' to your Digma Account URL on the User/Workspace level. Leave the port as 5051. 

![image](https://user-images.githubusercontent.com/93863/165008209-c832fc43-0600-48e9-9324-a5c9f8e4b904.png)

### Prepare the FastAPI app environment

1. Clone the repo and cd to the repo folder.

    ```sh
    cd path/to/repo
    ```

2. Optionally create and activate a virtualenv for the project. For example:

    ```sh
    python3 -m venv ./venv
    source venv/bin/activate
    ```

3. Install all the dependencies:

    ```sh
    pip install -r requirements.txt
    ```

4. In main.py, modify the OTEL exporter to use the Digma backend as well. For the `digma_backend` parameter in the Digma instrumentation replace `localhost` with the URL provided to your account, like so (do not include any brackets in the URL):

    ```python
    digma_opentelemetry_boostrap(
        service_name='server-ms',
        digma_backend="http://[ACCOUNT_URL]:5050",
        configuration=DigmaConfiguration().trace_this_package().set_environment('dev')
    )
    ```

5. Run the main file.

    ```sh
    python main.py
    ```

### Use the application

Play around to trigger some API calls. You can try visiting some of the API urls. 
For example:

- http://localhost:8000/users

Play around with the app and call some of the API urls.
You can find a helpful list of prepared HTTP requests in the [requests.http](requests.http) file.

We recommend installing the [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) (`humao.rest-client`) VS Code extension, which helps you call the urls in that file (including POST requests) and display their results directly in VS Code. You can also use [Postman](https://www.postman.com/downloads/) or other similar tools to call the urls.

### Troubleshooting

If you've encountered any issue, open the 'output' panel for the digma extension. It may contain more useful information about the issue:

![image](https://user-images.githubusercontent.com/93863/165012583-9d154ea5-7378-466b-a6cc-686d4b5261e3.png)
