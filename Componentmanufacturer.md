# Component manufacturers

As component manufacturer, your components will be part of other components and products. You are already providing your customers with documentations, manuals, data sheets and technical details.
To incentivize a circular value chain, you might already provide details about material composition, material origins and disassembly instructions. However, this information is probably only available on your website or part of component delivery.

To make your component part of the circular value chain, we propose to provide a DPP with relevant information about the component in the form of AAS.
You can find an example of a DPP for a Bosch servomotor here: [Download](https://market.aas-suite.com/api/Vws/download?id=38)

## DPP with AAS
This DPP was created with standardized templates provided by the IDTA: [Submodel Templates](https://industrialdigitaltwin.org/en/content-hub/submodels)

To create such a DPP, the AASX Package Explorer is the right tool. A detailed tutorial can be found here: [Screencasts](https://admin-shell-io.com/screencasts/)

The result will be a file describing your generic component. You can choose to create a file for each manufactured component (each instance) and provide information about the specific instance (serial numbers, manufacturing date).

## DPP service 
After the component is delivered, it will be used as part of the final product. In some use-cases, it might be important to include usage / maintenance data in the DPP of the component. That means, that the customer or the product manufacturer will update the DPP.
If you intend to host the DPP yourself, you can take the previously created DPP files and use AAS services like [FA³ST service](https://github.com/FraunhoferIOSB/FAAAST-Service) or [NOVAAS](https://gitlab.com/novaas/catalog/nova-school-of-science-and-technology/novaas).
To start FA³ST service, download the [newest version](https://repo1.maven.org/maven2/de/fraunhofer/iosb/ilt/faaast/service/starter/1.0.1/starter-1.0.1.jar) and type:
```sh
java -jar starter-{version}.jar -m your-component-aas.aasx
```
For docker, type:
```sh
docker run -v {path to your model file}:/model.json -e faaast.model=model.json fraunhoferiosb/faaast-service
```
For more details, click here: [documentation](https://faaast-service.readthedocs.io/en/latest/basics/usage.html)

## Data space 
To share this DPP with certified users of a data space, a data space connector like the [Eclipse Dataspace Connector](https://github.com/eclipse-edc/Connector) or [TRUE connector](https://github.com/Engineering-Research-and-Development/true-connector) is used.
Each company in a data space is certified by Identity Providers of the data space. The Identity Provider can be a wallet for decentralized identities to verify you in the data space. In this case, hosting this service: [IdentityHub](https://github.com/eclipse-edc/IdentityHub) is necessary. A simpler approach is a central IdentityProvider like Omejdn https://github.com/Fraunhofer-AISEC/omejdn-server. This server will be used to generate tokens with which access is verified. A traditional IdentityProvider can also be hosted with Keycloak, Hydra, etc.

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
and your EDC will automatically share the DPP stated in the properties file:
```sh
edc.aas.localAASModelPath=./example/resources/IDTA 02016-1-0 _Template_ControlComponentInstance.aasx
```
