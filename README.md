# How to use Conexiom Downloader

## Running

To run the downloader, double-click the `ConexiomDownloader.exe` file. This will automatically start downloading any files specified in the configuration file. The files that are downloaded will be placed in the folder on your computer that match the specifications in the `ConexiomDownloader.exe.config` file. An example is provided at the bottom of this README.


## Configuring

To configure what you download, the user that's downloading, or the server you're downloading from, open the `ConexiomDownloader.exe.config` file, then swap out the following options as specified below.

#### Changing the server

To change the server you're downloading from (specify a different IP address), edit the `<value>` area in following section:
```
<setting name="Host" serializeAs="String">
    <value>127.0.0.1</value>
</setting>
```
###
#### Changing the username

To change the user you're downloading as, edit the `<value>` area in the following section:

```
<setting name="Username" serializeAs="String">
    <value>PutYourUsernameHere</value>
</setting>
```
###

#### Changing the password

To change the password for the user you're downloading as, edit the `<value>` area in the following section:

```
<setting name="Password" serializeAs="String">
    <value>PutYourPassword&amp;Here</value>
</setting>
```

Note that in the above example, instead of `&` we use the encoded value of `&amp;`, since `xml` templates require certain special characters be escaped. To ensure your XML file will run correctly you can open the `ConexiomDownloader.exe.config` file in any XML editor and it should highlight areas that are the incorrect format or need to be replaced with encoded characters.
###
#### Changing where the files download

To specify where on your computer you want the files on the server to download, edit the `<value>` area in the following section:

```
<setting name="DownloadDir" serializeAs="String">
    <value>C:\WORK</value>
</setting>
```

With this setting, all files found when the connection is established will be downloaded to your local folder at `C:\WORK`.
###
#### Changing where the files download

To specify where on your computer you want the files on the server to download, edit the `<value>` area in the following section:

```
<setting name="SftpDir" serializeAs="String">
    <value>Prod/outbound</value>
</setting>
```

With the setting above, after you connect to the IP provided with the username and password provided, you will download all files specified in `Prod/outbound` on the server.
###
#### Deleting files from the server 

You can edit the `<value>` area in the following section to `True` or `False` (case-sensitive). If `True`, files that you download will be deleted from the server after the download completes.

```
<setting name="DeleteAfterDownload" serializeAs="String">
    <value>True</value>
</setting>
```


## Example

The example below will connect to server `123.123.120.11` with the username `JohnDoe` and the password `abc123`. It will find the `Test/outbound` directory and download every filter inside of the folder to the location `C:\WORK` on your computer. Afterwards, every file inside of `Test/outbound` will be deleted. 

```
    <ConexiomDownloader.Properties.Settings>
        <setting name="Host" serializeAs="String">
            <value>123.123.120.11</value>
        </setting>
        <setting name="Username" serializeAs="String">
            <value>JohnDoe</value>
        </setting>
        <setting name="Password" serializeAs="String">
            <value>abc123</value>
        </setting>
        <setting name="DownloadDir" serializeAs="String">
            <value>C:\WORK</value>
        </setting>
        <setting name="SftpDir" serializeAs="String">
            <value>Test/outbound</value>
        </setting>
        <setting name="DeleteAfterDownload" serializeAs="String">
            <value>True</value>
        </setting>
    </ConexiomDownloader.Properties.Settings>
```

## Other settings

You may specify no value inside the `SftpDir` setting, instead of a value like `Prod/outbound`. This will download everything from the top level directory. Beware using this with `DeleteAfterDownload`, however - after downloading every file in the top directory it will also follow suite and delete everything from that directory, so keep this in mind.

```
<setting name="SftpDir" serializeAs="String">
    <value></value> <!-- Root level folder after you connect to the server -->
</setting>
```
