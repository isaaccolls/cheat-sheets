<!-- MarkdownTOC autolink="true" levels="1,2" -->

- [install](#install)

<!-- /MarkdownTOC -->

# install

## Java

- install java 8

```bash
sudo apt install default-jre
sudo apt install default-jdk
```

- version `java -version` and `javac -version`
- Managing Java

```bash
sudo update-alternatives --config java
sudo update-alternatives --config javac <- this for javac
```

- Setting the **JAVA_HOME** Environment Variable
  - This command shows each installation of Java along with its installation path: `sudo update-alternatives --config java`
    - OpenJDK 8 is located at `/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java.`
  - Add it on **.zshrc**:

```bash
export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/"
export PATH=JAVA_HOME/bin:$PATH
```

- Test Enviroment variable `echo $JAVA_HOME`

## maven

- update packge index `sudo apt-get update`
- install maven `sudo apt-get install maven`
- verify the installation `mvn -version`

## spring tools

- download from [https://spring.io/tools](https://spring.io/tools)

```bash
sudo cp spring-tool-suite-4-4.3.0.RELEASE-e4.12.0-linux.gtk.x86_64.tar.gz /opt
cd /opt/
sudo tar zxvf spring-tool-suite-4-4.3.0.RELEASE-e4.12.0-linux.gtk.x86_64.tar.gz
sudo ln -s /opt/sts-4.3.0.RELEASE/SpringToolSuite4 /usr/local/bin/sts
```

- create launcher `sudo gedit /usr/share/applications/stsLauncher.desktop`

```
[Desktop Entry]
Name=Spring Tool Suite
Comment=Spring Tool Suite 4.3.0
Exec=/opt/sts-4.3.0.RELEASE/SpringToolSuite4
Icon=/opt/sts-4.3.0.RELEASE/icon.xpm
StartupNotify=true
Terminal=false
Type=Application
Categories=Development;IDE;Java;
```
