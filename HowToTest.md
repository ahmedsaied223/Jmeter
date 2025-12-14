# Prerequisites
## Install JMeter

Apache JMeter is an open-source software designed to load test functional behavior and measure performance. Here's how to install it on macOS:

## Installation Steps

### JMeter Prerequisites

Before you begin, ensure you have Java Development Kit (JDK) installed on your macOS. You can download and install the JDK 11 from the [official Oracle website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) or higher version of JDK.

a. **Download Apache JMeter:**

- Go to the [Apache JMeter download page](https://jmeter.apache.org/download_jmeter.cgi).
- Under the **Binaries** section, download the latest version of Apache JMeter.
- Alternatively, you can use `wget` or `curl` in the terminal to download. For example:

  ```sh
  wget https://downloads.apache.org/jmeter/binaries/apache-jmeter-5.6.3.zip
  ```

b. **Extract the Zip Archive:**

- Once the download is complete, locate the downloaded zip file.
- Right-click on the zip file and select "Open With" > "Archive Utility" or use the command line:

  ```sh
  unzip apache-jmeter-5.6.3.zip
  ```

c. **Move JMeter to a Preferred Location:**

- Move the extracted folder to a location of your choice. For example, you can move it to `/Applications`:

  ```sh
  mv apache-jmeter-5.6.3 /Applications/
  ```

d. **Set JMeter Home (Optional):**

- Setting up JMeter home makes it easier to run JMeter commands from the terminal. Add the following lines to your shell profile file (e.g., `~/.bash_profile`, `~/.bashrc`, `~/.zshrc`):

  ```sh
  export JMETER_HOME="/Applications/apache-jmeter-5.6.3"
  export PATH=$PATH:$JMETER_HOME/bin
  ```

e. **Run JMeter:**

- Start JMeter by running the `jmeter.sh` script if you have set up `$JMETER_HOME/bin` to `PATH`:

  ```sh
  jmeter.sh
  ```

- Alternatively, you can use the `jmeter` command directly if you have set up the `JMETER_HOME` variable:

  ```sh
  $JMETER_HOME/bin/jmeter
  ```

f. **Verify Installation:**

- Once JMeter starts, you should see the JMeter GUI.
- You can also check the version by clicking on "Help" > "About Apache JMeter".

g. **Install Plugin manager:**

- Go to https://jmeter-plugins.org/wiki/PluginsManager/ and download the [jar](https://jmeter-plugins.org/get/) file
- Put the downloaded jar file into JMeter's lib/ext directory
- Restart JMeter

h. **Install XML Plugins:**

- Go to JMeter UI -> Options -> Plugin Manager -> Available Plugins
- Search for `XML Plugins`
- It will list `XML Plugins` from Vendor `JMeter-Plugins.org`
- Select it and Click `Apply Changes and Restart JMeter` at the bottom

# How to run the load test?

a. **Run the test script SimulatorsLoadTest.jmx:**

- This test sets up 200 threads and sets a unique stream for each thread and fetches unique stream per thread/user for 10 seconds and deletes the stream.

  ```sh
  jmeter.sh -n -t ./SimulatorsLoadTest.jmx -l ./LoadTest10secs.jtl -Jsummary_report_file=LoadTestSummaryReport_10secs.csv
  ```

- This test has following three variables to customize the test. Use -Jvar=value
    - users (number of threads/users in the test)
    - run_time_seconds (duration each thread tries to fetch the manifest)
    - summary_report_file (summary report file location. suggested to keep it where the .jmx file resides or subdirectories of it)
    - To run the test for 600 seconds with 250 users and customize the .jtl and summary report file location, use the below command.
          ```sh
          jmeter.sh -n -t ./SimulatorsLoadTest.jmx -l ./LoadTest600seconds.jtl -Jusers=250 -Jrun_time_seconds=600 -Jsummary_report_file=LoadTestSummaryReport_600secs.csv
          ```

b. **How to run test bed test scripts?**

- Launch JMeter and select the desired test script
- Review the Environment: env_simulators which loads the config from configs/env-simulators.csv
    - Make sure clotho and simulators are running
    - Review the hostname and ports for delphi, packager simulators and clotho
- Run the test from JMeter UI and verify the results
