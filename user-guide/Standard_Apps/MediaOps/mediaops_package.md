---
uid: mediaops_package
---

# MediaOps install package

The MediaOps solution can be installed using one of the install packages from the Catalog.

> [!WARNING]
> As of today, the MediaOps solution has not officially been released, so a package is only available from Jenkins.
> Reach out to [MediaOps Support](mailto:support.mediaops@skyline.be) if you want to give it a try.

## Branches

There are 3 distinct branches of the MediaOps solution:

- **1.0.X**

The *1.0.X* branch installs the release of the MediaOps solution.

Once this package is installed, the solution needs to be configured from scratch before you can effectively use it.
This is the branch you need if you want to use the MediaOps solution at an environment with real equipment.

More details about the versioning of this package can be found in the [Versioning](xref:mediaops_versioning) page.

- **Demo**

The *Demo* branch is the branch that can be used to create additional demo data on top of the contents of the 1.0.X branch, and contains a prerelease of the components of the MediaOps solution.
If you want to play with the MediaOps solution, and have demo data available out-of-the-box, then this is the package you need.

- **Regression**

The *Regression* branch is similar to the demo branch, but is specifically used for the regression run of MediaOps. The only difference with the Demo branch, is that this one will have additional actions during the installation of the package to make sure the regression environment is fully setup for the regression run.

More details about the regression run are described in the [Regression](xref:mediaops_regression) page.

## Contents

### Scripts

The MediaOps scripts repository is available on [GitHub](https://github.com/SkylineCommunications/SLC-AS-MediaOps).

Additionally, some additional generic GQI custom operators, ad-hoc data sources, and scripts are included as in the package as well:

- [SLC-GQIOP-Format-Number](https://github.com/SkylineCommunications/SLC-GQIOP-Format-Number)
- [SLC-GQIO-RenameColumn](https://github.com/SkylineCommunications/SLC-GQIO-RenameColumn)
- [SLC-GQIO-AddColumns](https://github.com/SkylineCommunications/SLC-GQIO-AddColumns)
- [SLC-GQIDS-Dummy-Table](https://github.com/SkylineCommunications/SLC-GQIDS-Dummy-Table)
- [SLC-AS-Merge-App-Themes](https://github.com/SkylineCommunications/SLC-AS-Merge-App-Themes)

The regression tests are stored in a separate repository which is also available on [GitHub](https://github.com/SkylineCommunications/SLC-AS-MediaOps-RegressionTests).

### Applications

The applications part of the MediaOps package are described here: [MediaOps apps](xref:mediaops_apps).
These applications are stored in a CompanionFiles repository available at CompanionFiles\Generic\DataMiner Solutions\MediaOps.

### DOM model

The MediaOps DOM model is deployed using scripts that are part of the script repository.
Once the package has been installed, an additional script is triggered that will execute all necessary scripts that install or update the DOM modules on the DMS.
The files representing the DOM module are stored along with the apps in the CompanionFiles repository available at CompanionFiles\Generic\DataMiner Solutions\MediaOps.

The data model is documented [here](xref:mediaops_datamodel).

### Connectors

As the Demo and Regression branches need elements when used with the demo data, the following demo connectors are also included in this package:

- AMWA NMOS IS-05 (9001.0.0.X)
- Generic Switch (9100.0.0.X)
- Generic Matrix (9001.0.0.X)

Additionally, the Regression branch also includes the *"Skyline QAPortal"* connector which is used to report regression results to the QAPortal.

> [!NOTE]
> As the 1.0.X branch does not create any elements, these connectors are not part of that package.
> If you need specific connectors for a customer environment, then these need to be installed separately or a new package needs to be created including both the connectors and the 1.0.X MediaOps package.
