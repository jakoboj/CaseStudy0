# CaseStudy0

<h2>Create Users</h2>
Bob is assigned the Owner role of the ContosoCoffee resource group, and assigned Global Administrator to the Subscription. <br />
Dave is assigned the Contributor role to the resource group. <br />
Mark is assigned the Reader role to the resource group. <br />
<br />

<h2>Website hosting</h2>
I decided to host the web apps by pulling the web app template.
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
<ul>
  <li>
    Storage accounts > +Create > Performance: Standard > Redundancy: GRS > Review+create > Create
  </li>
  <li>
    Containers > +Container > Name: imagecontainer > Create
  </li>
  <li>
    imagecontainer > Shared access tokens > Give permissions > Set time > Generate SAS token and URL
  </li>
</ul>

<h2>ARM Template</h2>
In the template folder


