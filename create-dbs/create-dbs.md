# Crea un DBSystem HeatWave

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## Introducción

En este laboratorio, crearás y configurarás un DB System HeatWave.


_Tiempo estimado:_ 15 minutos

### Objetivos

En este laboratorio, serás guiado a través de las siguientes tareas:

- Creación de una Virtual Cloud Network
- Creación de una instancia de HeatWave (DB System)

### Prerequisitos

- Una cuenta de prueba o de pago de Oracle Cloud Infraestructure

## Task 1: Create Virtual Cloud Network

1. You should be signed in to Oracle Cloud!

    Click **Navigation Menu**,

    ![OCI Console Home Page](./images/homepage.png " home page")

2. Click  **Networking**, then **Virtual Cloud Networks**  
    ![menu vcn](./images/home-menu-networking-vcn.png "home menu networking vcn ")

    Select the root compartment
    ![vcn wizard Select Root compartment](./images/vcn-menu-compartmen-root.png "vcn menu compartmen root ")

3. Select the Click **Start VCN Wizard**
    ![vcn start wizard](./images/vcn-wizard-menu.png "vcn wizard menu")

4. Select 'Create VCN with Internet Connectivity'

    Click 'Start VCN Wizard'
    ![vcn wizard start create](./images/vcn-wizard-start.png "start vcn wizard start")

5. Create a VCN with Internet Connectivity

    On Basic Information, complete the following fields:

    VCN Name:

    ```bash
    <copy>HEATWAVE-VCN</copy>
    ```

    Compartment: Select  **(root)**

    Your screen should look similar to the following
    ![select compartment](./images/vcn-wizard-compartment.png "select compartment")

6. Click 'Next' at the bottom of the screen

7. Review Oracle Virtual Cloud Network (VCN), Subnets, and Gateways

    Click 'Create' to create the VCN
    ![create vcn](./images/vcn-wizard-create.png "create vcn")

8. When the Virtual Cloud Network creation completes, click 'View Virtual Cloud Network' to display the created VCN
    ![vcn creation completing](./images/vcn-wizard-view.png "vcn creation completing")

## Task 2: Configure security list to allow MySQL incoming connections

1. On HEATWAVE-VCN page under 'Subnets in (root) Compartment', click  '**Private Subnet-HEATWAVE-VCN**'
     ![vcn subnet](./images/vcn-details-subnet.png "vcn details subnet")

2. On Private Subnet-HEATWAVE-VCN page under 'Security Lists',  click  '**Security List for Private Subnet-HEATWAVE-VCN**'
    ![vcn private security list](./images/vcn-private-security-list.png "vcn private security list")

3. On Security List for Private Subnet-HEATWAVE-VCN page under 'Ingress Rules', click '**Add Ingress Rules**'
    ![vcn private subnet](./images/vcn-private-security-list-ingress.png "vcn private security list ingress")

4. On Add Ingress Rules page under Ingress Rule 1

    a. Add an Ingress Rule with Source CIDR

    ```bash
    <copy>0.0.0.0/0</copy>
    ```

    b. Destination Port Range

    ```bash
    <copy>3306,33060</copy>
     ```

    c. Description

    ```bash
    <copy>MySQL Port Access</copy>
    ```

    d. Click 'Add Ingress Rule'
    ![add ingres rule](./images/vcn-private-security-list-ingress-rules-mysql.png "vcn private security list ingress rukes mysql")

5. On Security List for Private Subnet-HEATWAVE-VCN page, the new Ingress Rules will be shown under the Ingress Rules List
    ![show ingres rule](./images/vcn-private-security-list-ingress-display.png "vcn private security list ingress display")

## Task 3: Configure security list to allow HTTP incoming connections

1. Navigation Menu > Networking > Virtual Cloud Networks

2. Open HEATWAVE-VCN

3. Click  public subnet-HEATWAVE-VCN

4. Click Default Security List for HEATWAVE-VCN

5. Click Add Ingress Rules page under Ingress Rule

    Add an Ingress Rule with Source CIDR

    ```bash
    <copy>0.0.0.0/0</copy>
    ```

    Destination Port Range

    ```bash
    <copy>80,443</copy>
    ```

    Description

    ```bash
    <copy>Allow HTTP connections</copy>
    ```

6. Click 'Add Ingress Rule'

    ![Add HTTP Ingress Rule](./images/vcn-ttp-add-ingress.png "Add HTTP Ingress Rule")

7. On Security List for Default Security List for HEATWAVE-VCN page, the new Ingress Rules will be shown under the Ingress Rules List

    ![View VCN Completed HTTP Ingress rules](./images/vcn-ttp-ingress-completed.png "View VCN Completed HTTP Ingress rules")

## Task 4: Create MySQL Database for HeatWave (DB System) instance

1. Click on Navigation Menu
         Databases
         MySQL
    ![home menu mysq](./images/home-menu-database-mysql.png "home menu mysql")

2. Click 'Create DB System'
    ![mysql create button](./images/mysql-menu.png " mysql create button")

3. Create MySQL DB System dialog by completing the fields in each section

    - Provide DB System information
    - Setup the DB system
    - Create Administrator credentials
    - Configure Networking
    - Configure placement
    - Configure hardware
    - Exclude Backups
    - Set up Advanced Options

4. For DB System Option Select **Development or Testing**

    ![heatwave db option](./images/mysql-create-option-develpment.png "heatwave db option")

5. Provide basic information for the DB System:

    a. Select Compartment **(root)**

    b. Enter Name

    ```bash
    <copy>HEATWAVE-DB</copy>
    ```

    c. Enter Description

    ```bash
    <copy>MySQL HeatWave Database Instance</copy>
    ```

    d. Select **Standalone** and enable **Configure MySQL HeatWave**
    ![heatwave db info setup](./images/mysql-create-info-setup.png "heatwave db info setup ")

6. Create Administrator Credentials

    **Enter Username** (write username to notepad for later use)

    **Enter Password** (write password to notepad for later use)

    **Confirm Password** (value should match password for later use)

    ![heatwave db admin](./images/mysql-create-admin.png "heatwave db admin ")

7. On Configure networking, keep the default values

    a. Virtual Cloud Network: **HEATWAVE-VCN**

    b. Subnet: **Private Subnet-HEATWAVE-VCN (Regional)**

    c. On Configure placement under 'Availability Domain'

    Select AD-1  ...  Do not check 'Choose a Fault Domain' for this DB System.

    ![heatwave db network ad](./images/mysql-create-network-ad.png "heatwave db network ad ")

8. On Configure hardware
    - a. Click the **Change shape** button to select the **MySQL.HeatWave.VM.Standard** shape.
    - b. For Data Storage Size (GB) Set value to:  **1024**

    ![heatwave db  hardware](./images/mysql-create-db-hardware.png "heatwave db hardware ")

9. On Configure Backups, disable 'Enable Automatic Backup'

    ![heatwave db  backup](./images/mysql-create-backup.png " heatwave db  backup")

10. Click on Show Advanced Options

11. Go to the Networking tab, in the Hostname field enter (same as DB System Name):

    ```bash
        <copy>HEATWAVE-DB</copy> 
    ```  

    ![heatwave db advanced](./images/mysql-create-advanced.png "heatwave db advanced ")

12. Review **Create MySQL DB System**  Screen

    ![heatwave db create](./images/mysql-create.png "heatwave db create ")
  

    Click the '**Create**' button

13. The New MySQL DB System will be ready to use after a few minutes

    The state will be shown as 'Creating' during the creation
    ![show creeation state](./images/mysql-create-in-progress.png "show creeation state")

14. The state 'Active' indicates that the DB System is ready for use

    On HEATWAVE-HW Page, check the MySQL Endpoint (Private IP Address)

    ![heatwave endpoint](./images/mysql-detail-active.png "heatwave endpoint")

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, July 2023