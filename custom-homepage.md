custom-homepage

Custom Homepage
Dataverse allows you to use a custom homepage or welcome page in place of the default root dataverse page. This allows for complete control over the look and feel of your installation’s homepage.

Download this sample: custom-homepage.html and place it at /var/www/dataverse/branding/custom-homepage.html.

Once you have the location of your custom homepage HTML file, run this curl command to add it to your settings:

curl -X PUT -d '/var/www/dataverse/branding/custom-homepage.html' http://localhost:8080/api/admin/settings/:HomePageCustomizationFile

If you prefer to start with less of a blank slate, you can download the custom-homepage-dynamic.html template which was built for the Harvard Dataverse, and includes branding messaging, action buttons, search input, subject links, and recent dataset links. This page was built to utilize the Metrics API to deliver dynamic content to the page via javascript.

Note that the custom-homepage.html and custom-homepage-dynamic.html files provided have multiple elements that assume your root dataverse still has an alias of “root”. While you were branding your root dataverse, you may have changed the alias to “harvard” or “librascholar” or whatever and you should adjust the custom homepage code as needed.

For more background on what this curl command above is doing, see the “Database Settings” section below. If you decide you’d like to remove this setting, use the following curl command:

curl -X DELETE http://localhost:8080/api/admin/settings/:HomePageCustomizationFile