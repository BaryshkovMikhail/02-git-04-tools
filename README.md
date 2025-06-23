# Домашнее задание к занятию «Инструменты Git» - Барышков Михаиля

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.
2. Ответьте на вопросы.

- Какому тегу соответствует коммит 85024d3?
- Сколько родителей у коммита b8d720? Напишите их хеши.
- Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.
- Найдите коммит, в котором была создана функция func providerSource, её определение в коде выглядит так: func providerSource(...) (вместо троеточия перечислены аргументы).
- Найдите все коммиты, в которых была изменена функция globalPluginDirs.
- Кто автор функции synchronizedWriters?

В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.

## Решение

1. git show aefea --pretty=format:"%H %s" --no-patch

Полный хеш: aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Комментарий: Update CHANGELOG.md

2. -  Какому тегу соответствует коммит 85024d3?

```bash
git tag --contains 85024d3
```
v0.12.23

v0.12.24

v0.12.25

v0.12.26

v0.12.27

v0.12.28

v0.12.29

v0.12.30

v0.12.31

```bash
git describe --contains --exact-match 85024d3
```

v0.12.23^0


- Сколько родителей у коммита b8d720? Напишите их хеши.

```bash
git show --pretty=%P b8d720 -s
```

Родителей: 2

Хеши родителей:
- 56cd7859e05c36c06b56d013b55a252d0bb7e158
- 9ea88f22fc6269854151c571162c5bcf958bee2b


 Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.

```text
33ff1c03bb960b332be3af2e333462dde88b279e v0.12.24
b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release
```

- Найдите коммит, в котором была создана функция func providerSource(...).

```bash
git log -S 'func providerSource(' --pretty=format:"%H %s"
```

Хеш коммита: 8c928e83589d90a031f811fae52a81be7153e82f
Комментарий: main: Consult local directories as potential mirrors of providers

- Найдите все коммиты, в которых была изменена функция globalPluginDirs.

```bash
git log -G 'globalPluginDirs' --pretty=format:"%H %s"
```

```text
7c4aeac5f30aed09c5ef3198141b033eea9912be stacks: load credentials from config file on startup (#35952)
22a2580e93170eac46621ab97decaec989d52edb main: Use the new cliconfig package credentials source
35a058fb3ddfae9cfee0b3893822c9a95b920f4c main: configure credentials from the CLI config file
c0b17610965450a89598da491ce9b6b5cbd6393f prevent log output during init
8364383c359a6b738a436d1b7745ccdce178df47 Push plugin discovery down into command package
```

- Кто автор функции synchronizedWriters?

```bash
git log -S 'func synchronizedWriters(' --pretty=format:"%an"
```

```text 
James Bardin
Martin Atkins
```

Дополнительная проверка (если нужно уточнить, кто именно создал функцию):
Можно посмотреть первое упоминание функции в истории Git:

```bash 
git log --reverse -S 'func synchronizedWriters(' --pretty=format:"%H %an" | head -1
```

```text 
5ac311e2a91e381e2f52234668b49ba670aa0fe5 Martin Atkins
```