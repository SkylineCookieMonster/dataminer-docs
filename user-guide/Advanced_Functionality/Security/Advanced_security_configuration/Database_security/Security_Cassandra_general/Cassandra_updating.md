---
uid: Cassandra_updating
---

# Updating Cassandra

## Checking the Cassandra version

It is recommended to periodically update your Cassandra database. This will ensure that all known vulnerabilities are fixed.

To check the Cassandra version, go to *C:\Program Files\Cassandra\bin* and execute the following *nodetool* command:

   `.\nodetool version`

With recent DataMiner versions, **Cassandra 3.11** is installed by default. This is also the minimum supported version. Cassandra 4.0 is also supported.

> [!NOTE]
> Cassandra 4.0 **no longer supports Windows**. This means that extra Linux servers will be required to host the Cassandra database.

> [!TIP]
> To limit the impact of a breach through Cassandra, it is recommended to run the Cassandra service as a non-SYSTEM user. For more details, see [Running Cassandra as non-SYSTEM user](xref:Running_Cassandra_as_non-SYSTEM_user).

## Updating the Cassandra version

As with all software, it is good practice to ensure you are running the latest version to minimize the number of known vulnerabilities.

> [!TIP]
> A PowerShell script is available to update Cassandra easily. For more details see [Cassandra Hardening](https://github.com/SkylineCommunications/cassandra-hardening).

To update the Cassandra version:

1. Ensure you have a **full backup** of the Cassandra database.
1. Download the latest Cassandra *3.11.X* binaries from the [official website](https://cassandra.apache.org/_/download.html) and *extract* the archive.
1. Stop the DataMiner agent.
1. Push all data from memory to disk. Go to the *C:\Program Files\Cassandra\bin* folder and run the following command:
   `.\nodetool upgradesstables`
1. Stop the Cassandra service.
1. Rename the *C:\Program Files\Cassandra* folder to *Cassandra_bak*.
1. Create a new folder named *Cassandra* in *C:\Program Files*.
1. Copy the downloaded Cassandra binaries to this new *Cassandra* folder.
1. Copy the **old** *Java* folder from *C:\Program Files\Cassandra_bak\Java* to *C:\Program Files\Cassandra*.
1. Copy the **old** *cassandra.yaml* from *C:\Program Files\Cassandra_bak\conf\cassandra.yaml* to *C:\Program Files\Cassandra\conf*.
1. Copy the **old** *daemon* folder from *C:\Program Files\Cassandra_bak\bin\daemon* to *C:\Program Files\Cassandra\bin*.
1. Copy the **old** *DevCenter* folder from *C:\Program Files\Cassandra_bak\DevCenter* to *C:\Program Files\Cassandra*.
1. Create a new folder named *logs* in *C:\Program Files\Cassandra*.
1. To enable the use of *nodetool*, set the system-wide environment variables *JAVA_HOME* and *CASSANDRA_HOME* to the correct locations by executing the following PowerShell commands:

   `[System.Environment]::SetEnvironmentVariable('CASSANDRA_HOME','C:\progra~1\Cassandra\',[System.EnvironmentVariableTarget]::Machine)`

   `[System.Environment]::SetEnvironmentVariable('JAVA_HOME','C:\progra~1\Cassandra\Java\',[System.EnvironmentVariableTarget]::Machine)`

1. Open a PowerShell prompt (as Administrator) and execute the following command to register the Cassandra service:

   `cd 'C:\Program Files\Cassandra\bin\'; .\cassandra.ps1 -install`

1. To make sure the location of the *Jvm* is correctly set in the registry, execute the following PowerShell command:

   `Set-ItemProperty -Path "HKLM:\SOFTWARE\WOW6432Node\Apache Software Foundation\Procrun 2.0\cassandra\Parameters\Java" -Name "Jvm" -Value "C:\Program Files\Cassandra\Java\bin\server\jvm.dll"`

1. To prevent startup issues, DataMiner enables the commitlog.ignorereplayerrors option in Cassandra. Make sure this is set by executing the following PowerShell commands:

   `$options = Get-ItemProperty -Path "HKLM:\SOFTWARE\WOW6432Node\Apache Software Foundation\Procrun 2.0\cassandra\Parameters\Java" -Name "Options"`

   `$options.Options += "-Dcassandra.commitlog.ignorereplayerrors=true"`

   `Set-ItemProperty -Path "HKLM:\SOFTWARE\WOW6432Node\Apache Software Foundation\Procrun 2.0\cassandra\Parameters\Java" -Name "Options" -Value $options.Options`

1. Verify that the *Cassandra* service has been created and that it can be started from the task manager (or the service manager).

1. After a Cassandra upgrade, it is (sometimes) necessary to execute *nodetool upgradesstables* on your nodes to convert sstables to the new Cassandra version. Go to the *C:\Program Files\Cassandra\bin* folder and run the following command:

   `.\nodetool upgradesstables`

   > [!WARNING]
   > Depending on the size of your database, converting the sstables can take a while.

1. Start the DataMiner Agent and make sure that no error alarms are visible in the Alarm Console.

> [!TIP]
> After starting the Cassandra service, verify that the expected Cassandra version is logged in *C:\Program Files\Cassandra\Logs\system.log*. For example: *Cassandra version: 3.11.12*
> If the service does not start and no logs are created, make sure that the *Jvm* registry key refers to the correct location.
> Execute `nodetool status` to check whether the system is running stable. 
