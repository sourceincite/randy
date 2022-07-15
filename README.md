# Randy

## What

This is a pre-authenticated RCE exploit for Inductive Automation Ignition that impacts versions <= 8.1.16. We failed to exploit the bugs at Pwn2Own Miami 2022 because we had a sloppy exploit and no debug environment, but since then we have found the time and energy to improve it!

## Authors

Chris Anastasio and Steven Seeley (mr_me) of Incite Team

## Build

1. Build with `mvn clean compile assembly:single -DskipTests`

## Tested

The exploit was tested against [8.1.16](https://inductiveautomation.com/downloads/archive/8.1.16) using the Windows 64-bit Installer which you can [download here](https://files.inductiveautomation.com/release/ia/8.1.16/20220405-1206/ignition-8.1.16-windows-64-installer.exe) (SHA1: f135d32228793c73c4cdd88561cdbdb44b19290c) but it has known to work against other older versions as well.

## Notes

- At the time of release, no CVE's were assigned to the bugs
- This exploit takes advantage of two vulnerabilities that have been [patched](https://support.inductiveautomation.com/hc/en-us/articles/7625759776653):

  1. [GatewaySessionManagerImpl Authentication Bypass](https://srcincite.io/advisories/src-2022-0013/)
  2. [ScriptInvoke Remote Code Execution](https://srcincite.io/advisories/src-2022-0014/)

- The exploit requires an admin user to be logged into the gateway. During testing it was found that sessions live forever unless a user explicitly logs out.
- The exploit should be ran from a Windows host (due to the `SecureRandom` seed prediction attack).
- The exploit targets Ignition deployed under Windows, since `SecureRandom` is not so secure under that environment.
- The exploit was tested with Java v11.0.11.

## Run

Run the exploit with `java -cp target/randy-0.0.1-SNAPSHOT.jar com.srcincite.ia.exploit.Poc`

## Example

![Running Randy](/images/poc.png)
