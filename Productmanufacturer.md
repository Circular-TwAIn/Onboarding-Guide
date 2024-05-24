# Product manufacturers

As product manufacturer, you are already providing your customers with documentations, manuals, data sheets and technical details.
To incentivize a circular value chain, you might already provide details about material composition, material origins and disassembly instructions. However, this information is probably only available on your website or part of product delivery.

To make your product part of the circular value chain, we propose to provide a DPP with relevant information about the product in the form of AAS.
You can find an example of a DPP for a food machine here: [DPP machine](https://market.aas-suite.com/api/Vws/download?id=78)

## DPP with AAS
This DPP was created with standardized templates provided by the IDTA: [Submodel templates](https://industrialdigitaltwin.org/en/content-hub/submodels)

To create such a DPP, the AASX Package Explorer is the right tool. A detailed tutorial can be found here: [Screencast](https://admin-shell-io.com/screencasts/)

Your product might include other components, that can be described in the DPP. For this, a hierarchical structure referencing other DPPs can be created with the template "Hierarchical structures". If you received AAS for certain components in your product, reference them with the [SMT Hierarchical Structures](https://github.com/admin-shell-io/submodel-templates/tree/main/published/Hierarchical%20Structures%20enabling%20Bills%20of%20Material/1/0)

If no AAS is available, you can create a component-specific AAS or Submodel in your modeling.

The result will be a file describing your generic product. You can choose to create a file for each manufactured product (each instance) and provide information about the specific instance (serial numbers, manufacturing date).



## DPP service 
After the product is delivered, it will be used by the customer. In some use-cases, it might be important to include usage / maintenance data in the DPP of the product. That means, that the customer could send back data to your DPP.
If you intend to host the DPP yourself, you can take the previously created DPP files and use AAS services like [FA³ST service](https://github.com/FraunhoferIOSB/FAAAST-Service) or [NOVAAS](https://gitlab.com/novaas/catalog/nova-school-of-science-and-technology/novaas).
To start FA³ST service, download the [newest version](https://repo1.maven.org/maven2/de/fraunhofer/iosb/ilt/faaast/service/starter/1.0.1/starter-1.0.1.jar) and type:
```sh
java -jar starter-{version}.jar -m your-product-aas.aasx
```
For docker, type:
```sh
docker run -v {path to your model file}:/model.json -e faaast.model=model.json fraunhoferiosb/faaast-service
```
For more details, click here: [documentation](https://faaast-service.readthedocs.io/en/latest/basics/usage.html)

## Data space 
To share this DPP with certified users of a data space, a data space connector like the [Eclipse Dataspace Connector](https://github.com/eclipse-edc/Connector) or [TRUE connector](https://github.com/Engineering-Research-and-Development/true-connector) is used.
Each company in a data space is certified by the Identity Provider of the data space. The Identity Provider will create a certificate file for your connector to verify you in the data space. If no Identity Provider is available, you can choose to become the Identity Provider by hosting this service: [IdentityHub](https://github.com/eclipse-edc/IdentityHub)

If you choose the Eclipse Dataspace Connector as your connector, CircularTwAIn provides an easy-to-use EDC extension to share your DPP with less effort:
[EDC Extension for AAS](https://github.com/Circular-TwAIn/EDC-Extension-for-AAS)

Download the code and type:
```sh
cd /EDC-Extension-for-AAS
./gradlew clean build
```

After that, type:
```sh
java -Dedc.fs.config=./example/configurations/provider.properties -jar ./example/build/libs/dataspace-connector.jar
``` 
Your EDC will be started and automatically share the DPP stated in the properties file:
```sh
edc.aas.localAASModelPath=./example/resources/IDTA 02016-1-0 _Template_ControlComponentInstance.aasx
```
