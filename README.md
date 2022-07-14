# Randy

## What

This is a pre-authenticated RCE exploit for Inductive Automation Ignition that impacts versions <= 8.1.16. We failed to exploit the bugs at Pwn2Own Miami 2022 because we had a sloppy exploit and no debug environment, but since then we have found the time energy to improve it!

## Authors

Chris Anastasio and Steven Seeley (mr_me) of Incite Team

## Build

1. Build with `mvn clean compile assembly:single`

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

Run the exploit with `java -cp "libs/*";"target/exploit-0.0.1-SNAPSHOT.jar" com.srcincite.ia.exploit.Poc`

## Example

![Running Randy](/images/poc.png)
