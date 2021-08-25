# CaseStudy0

![Diagram](https://github.com/jakoboj/CaseStudy0/blob/main/Screenshots/Diagram.PNG)

<h2>Create Users</h2>
Bob is assigned the Owner role of the ContosoCoffee resource group, and assigned Global Administrator to the Subscription. <br />
Dave is assigned the Contributor role to the resource group. <br />
Mark is assigned the Reader role to the resource group. <br />
<br />

<h2>Website hosting</h2>
I decided to host the web apps by pulling the CoffeeTemplate from github.
<h3>What I did</h3>
<ul>
  <li>
    App Services > +Create > Name: ContosoCoffeeUK > Runtime stack: .NET Core 3.1 > Region: UK South
  </li>
  <li>
    App Services > +Create > Name: ContosoCoffeeUS > Runtime stack: .NET Core 3.1 > Region: East US
  </li>
  <br />
  <li>
    App Service > ContosoCoffeeUK > Deployment Center > Pull forked repository from GitHub
  </li>
  <li>
    <b>Do same for ContosoCoffeeUS</b>
  </li>
  <br />
  <li>
    contosocoffeeuk.azurewebsites.net & contosocoffeeus.azurewebsites.net is now up and running
  </li>
</ul>
<br />

<h2>Load Balancing and Geo-redundent access</h2>
<b>Note!</b> <i>Traffic Manager did not work properly for me, even though I configured it correctly.</i>
<br />
To direct users to the closest server (or best performance), I've used a Traffic Manager Template
<br />
<h3>What I did</h3>
<ul>
  <li>
    Traffic Manager Profile > +Create > Name: bobscoffee > Routing Method: Performance > Subscription: Azure Pass > Resource Group: ContosoCoffee > Create
  </li>
  <li>
    bobscoffee > Endpoints > +Add > Type: Azure endpoint > Name: contosocoffeeus or contosocoffeeuk > Target resource type: App Service > Target resource > Depends on name (uk or us) > Add
  </li>
  
  <li>
    bobscoffee.trafficmanager.net shows 404 Website not found, even though it should be configured correctly
  </li>
</ul>
<br />
    
<h2>Contoso Coffee data storage</h2>
To store data, I've created a blob storage account, with a blob storage container. To make sure the storage account automatically archive data to slower storage when required, I've added a Lifecycle management rule, which archives data if its not been modified in 90 days. I've also created a SAS key for a future image gallery.
<br />
<ul>
  <li>
    Storage accounts > +Create > Performance: Standard > Redundancy: GRS > Review+create > Create
  </li>
  <li>
    Storage accounts > Lifecycle management > +Add a rule > If Baseblobs havent been modified in 90 days Then Move to archive storage
  </li>
  <li>
    Containers > +Container > Name: imagecontainer > Create
  </li>
  <li>
    imagecontainer > Shared access tokens > Give permissions > Set time > Generate SAS token and URL
  </li>
</ul>
<br />

<h2>ARM Template</h2>
In the arm-template file


