<h1>5 minutes, migrate your Phantom Beast Palu server to the computing nest </h1>

<p> players who use the computing nest key to build the magic beast palu server can directly interface and modify the
    configuration of death drop on the console.
    However, if you create ECS and install the magic beast palu server through ECS extension (OOS), you will not have
    these interface management functions and need to log in to the server to manually modify the configuration file,
    which is very inconvenient. </p>

<p> to solve this problem, computing nest now supports migrating your magic beast palu server to computing nest for
    management, so that you can also manage configuration items and upgrade game servers through the interface. </p>

<p> The upgrade process is very simple, just three steps:

    1. Backup Archive
    2. Create computing nest magic beast Palu management service
    3. Restore Archive </p>

<p> If your original Phantom Beast Palu server has not been archived, then you only need to do one step: create a
    computing nest to manage the Phantom Beast Palu service. </p>

<hr/>

<h2>1. Backup archive (skip without archive)</h2>

<p> In order to use the computing nest's ability to manage the Phantom Beast Palu server, the computing nest needs to
    reset your ECS server to the operating system image customized by the computing nest.
    Therefore, if you already have an archive on your server, it is recommended to back up the archive first in order to
    avoid your efforts and those of Palu being wasted. </p>

<h3>1.1 Palworld archive backup of Windows system </h3>

<p> if you originally installed the magic beast palu server through ECS extension (OOS) and the operating system is
    Windows, you can find the server archive of magic beast palu under this path:</p><pre><code>C:\Program Files\PalServer\steam\steamapps\common\PalServer\Pal\Saved</code></pre>

You can log in to the ECS server through a remote connection, package and download the directory to the local for
backup.Specific operation:
1. Visit the <a href="https://ecs.console.aliyun.com/server">ECS console </a>, find your server, and click <strong>
    Remote Connection </strong> > <strong> Login Now </strong>. Be careful not to choose secret-free landing.

2. You need to stop the game service before backing up to ensure that all game progress has been written to the
archive. You can stop the game service by executing this command in the PowerShell.<pre><code>Get-Process -name PalServer-Win64-Test-Cmd | Stop-Process</code></pre>

3. Find the archive location and package the archive directory into a zip package.

4. Drag the compressed archive file to the workbench\Download directory, it will trigger the browser's file download,
and then download it to the local.
<hr/>

### 1.2 Palworld Archive Backup for Linux Systems

If you originally installed the Phantom Beast Palu server through ECS extension (OOS) and the operating system is Linux,
you can find the server archive of Phantom Beast Palu under this path:
<pre><code>/PalSaved</code></pre>
You can remotely log on to the ECS server, package and download the directory to the local for backup.
Specific operation:

1. Visit the [ECS console](https://ecs.console.aliyun.com/server), find your server, and click **Remote Connection**> **Login Now * *.

2. Find the archive location and use the following command to package the archive:
   <pre><code># Before migrating, please stop the game service to ensure the migration is successful
   docker stop palworld-server
   # If you are prompted to command not found, zip is not installed, you can try to execute yum install zip first
   zip -r /PalSaved.zip /PalSaved
   </code></pre>

3. After the package is completed, click the file in the upper left corner of the ECS remote connection page,
and <strong> open the file tree </strong>. Right-click the packaged/PalSaved.zip file and select <strong> Download
    File </strong>. </p>

<hr/>

<h2>2. Create a computing nest Phantom Beast Palu management service (migrate to computing nest)</h2>

<p> This step is very simple, you only need to complete it according to the interface guidance of the calculation nest.
    Specific operation:
    1. Visit <a
            href="https://computenest.console.aliyun.com/service/instance/create/cn-hangzhou?type=user&ServiceId=service-959ba5511d6c481fbb50">
        Computing Nest Phantom Beast Palu Management Service </a>.
    2. Then select the server you need to migrate and complete the creation according to the guidelines. </p>

<p><img src="images/en_2.jpg" width="1000"/></p>

<p> Wait for about 5 minutes, the task will be completed, and then you can get the new server IP and port here. </p>

<p><img src="images/en_2.jpg" width="1000"/></p>

<hr/>

<h2>3. Restore Archive </h2>

<p> After the upgrade is complete, you can go to the service instance details page. Archive import is completed through
    the Import Archive function on the interface. </p>

<p><img src="images/restore_archive.jpg" width="1000"/></p>

<p> wait for the task to be completed, then you can start the game. </p>

<h2>4. Frequently Asked Questions </h2>

<h3>4.1 why can I log in to the game after upgrading, but I lost the line after a while?</h3>

<h4> Reason (Skip if you don't understand)</h4>

<p> This problem usually occurs under Linux. Because the computing nest builds the magic beast palu server, the linux
    user running the PalServer behind it is ecs-assist-user, and you may use root to operate the archive file, causing
    the ParServer to be unable to write the archive, and the program will crash if you cannot write the archive file by
    taking a few steps. </p>

<h4> Processing method </h4>

<p> You need to connect to the linux server remotely, and then execute:</p>

<code>chown -R ecs-assist-user:ecs-assist-user /home/ecs-assist-user/.steam/steam/SteamApps/common/PalServer/Pal/Saved
</code>