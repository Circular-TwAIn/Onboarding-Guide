# Customer

As customer, you want to access the DPP, for example for more information on the materials in your product or how to disassemble a battery.

## Access DPP with data space
The DPPs are created with standardized AAS templates provided by the IDTA: [Submodel templates](https://industrialdigitaltwin.org/en/content-hub/submodels)
To access those DPP, a data space connector like the [Eclipse Dataspace Connector](https://github.com/eclipse-edc/Connector) or [TRUE connector](https://github.com/Engineering-Research-and-Development/true-connector) is used.
Each company in a data space is certified by Identity Providers of the data space. The Identity Provider can be a wallet for decentralized identities to verify you in the data space. In this case, hosting this service: [IdentityHub](https://github.com/eclipse-edc/IdentityHub) is necessary. A simpler approach is a central IdentityProvider like Omejdn https://github.com/Fraunhofer-AISEC/omejdn-server. This server will be used to generate tokens with which access is verified. A traditional IdentityProvider can also be hosted with Keycloak, Hydra, etc.

If you choose the Eclipse Dataspace Connector as your connector, CircularTwAIn provides an easy-to-use EDC extension to access a DPP with less effort:
[EDC Extension for AAS](https://github.com/Circular-TwAIn/EDC-Extension-for-AAS)

Download the code and navigate to the example:
```sh
cd /EDC-Extension-for-AAS
cd /example
```

After that, use Docker compose and type:
```sh
docker-compose up
``` 
Your EDC will be started and you can access a DPP by using the included "Automated negotiation" request in the 
[Postman collection](https://github.com/FraunhoferIOSB/EDC-Extension-for-AAS/blob/main/example/resources/aas_edc_extension.postman_collection.json).

For more details, check our 
[example](https://github.com/FraunhoferIOSB/EDC-Extension-for-AAS/tree/main/example).
