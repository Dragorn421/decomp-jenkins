# Decomp Jenkins Agent Dockerfile

This repo contains the `Dockerfile` used to create a [Jenkins Agent](https://www.jenkins.io/doc/book/using/using-agents/) that contains the programs and packages used in a number of Decomp projects.

## Running the Jenkins Agent

Create a `roms` directory and add the relevant ROMs to it:

```sh
mkdir -p roms
cp some_roms_here roms/
```

Spin up a Docker container, mounting in the `roms` directory that you just created

**NOTE:** Replace `MY_SECRET` and `MY_AGENT_NAME` with your given secret and agent name.

```sh
docker run \
    -v "$(pwd)"/roms:/usr/local/etc/roms \
    --init ghcr.io/ethteck/decomp-jenkins:latest \
    -url https://jenkins.deco.mp/ MY_SECRET MY_AGENT_NAME
```

**NOTE:** You can pass the `--detach` argument to `docker run` to run the container in the background.

## Supported ROMs

Below are the supported ROMs and their filenames. They should be placed in your `roms` directory.

| Game (version)   | Desired filename     | SHA1 Hash                                  |
| ---------------- | -------------------- | ------------------------------------------ |
| OOT MQ Debug     | oot-gc-eu-mq-dbg.z64 | `bdd50f5e84d6fe2683dac92de3fd0485c06c1b51` |
| OOT GC PAL MQ    | oot-gc-eu-mq.z64     | `f46239439f59a2a594ef83cf68ef65043b1bffe2` |
| OOT GC PAL       | oot-gc-eu.z64        | `0227d7c0074f2d0ac935631990da8ec5914597b4` |
| MM US            | mm.us.rev1.z64       | `d6133ace5afaa0882cf214cf88daba39e266c078` |
| Paper Mario JP   | papermario.jp.z64    | `b9cca3ff260b9ff427d981626b82f96de73586d3` |
| Paper Mario US   | papermario.us.z64    | `3837f44cda784b466c9a2d99df70d77c322b97a0` |
| Paper Mario PAL  | papermario.us.z64    | `2111d39265a317414d359e35a7d971c4dfa5f9e1` |
| Paper Mario iQue | papermario.cn.z64    | `5c724685085eba796537573dd6f84aaddedc8582` |
| TMC Demo JP      | tmc.demo.jp.gba      | `9cdb56fa79bba13158b81925c1f3641251326412` |
| TMC Demo US      | tmc.demo.gba         | `63fcad218f9047b6a9edbb68c98bd0dec322d7a1` |
| TMC EU           | tmc.eu.gba           | `cff199b36ff173fb6faf152653d1bccf87c26fb7` |
| TMC JP           | tmc.jp.gba           | `6c5404a1effb17f481f352181d0f1c61a2765c5d` |
| TMC US           | tmc.us.gba           | `b4bd50e4131b027c334547b4524e2dbbd4227130` |
| Animal Forest JP | af.jp.z64            | `e106dff7146f72415337c96deb14f630e1580efb` |
| Pokemon Snap US  | pokemonsnap.us.z64   | `edc7c49cc568c045fe48be0d18011c30f393cbaf` |

## Building image locally

If you wish to make changes to the `Dockerfile`, you can build your own version of the image:

```sh
docker build . -t decomp-jenkins
```
