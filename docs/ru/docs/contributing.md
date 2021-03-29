# Развитие проекта - Как внести свой вклад?

Во-первых, возможно вы захотите узнать как [помочь FastAPI или получить помощь](help-fastapi.md){.internal-link target=_blank}.

## Разработка проекта

Если вы уже склонировали репозиторий и знаете, что вам нужно будет глубже погрузиться в кодовую базу, вот несколько рекомендаций по настройке вашей виртуальной среды среды.

### Виртуальная среда `venv`

Вы можете создать виртуальное окружение с использованием питоновского модуля `venv`:

<div class="termy">

```console
$ python -m venv env
```

</div>

Это создаст директорию `./env/` содержащую бинарные файлы Python после чего вы сможете устанавливать пакеты для данной изолированной среды.

### Активация виртуальной среды

Активируйте созданное вами окружение с помощью:

=== "Linux, macOS"

    <div class="termy">

    ```console
    $ source ./env/bin/activate
    ```

    </div>

=== "Windows PowerShell"

    <div class="termy">

    ```console
    $ .\env\Scripts\Activate.ps1
    ```

    </div>

=== "Windows Bash"

   Или же если вы используете Bash для Windows (пример: <a href="https://gitforwindows.org/" class="external-link" target="_blank">Git Bash</a>):

    <div class="termy">

    ```console
    $ source ./env/Scripts/activate
    ```

    </div>

Чтобы проверить работу виртуального окружения используйте:

=== "Linux, macOS, Windows Bash"

    <div class="termy">

    ```console
    $ which pip

    some/directory/fastapi/env/bin/pip
    ```

    </div>

=== "Windows PowerShell"

    <div class="termy">

    ```console
    $ Get-Command pip

    some/directory/fastapi/env/bin/pip
    ```

    </div>

Если вы увидите бинарный файл `pip` в директории `env/bin/pip` значит всё работает. 🎉



!!! Примечание
    Каждый раз когда вы устанавливаете новый пакет используя `pip` в данной виртуальной среде, сделайте перезапустите её.

    Это позволит удостовериться, что запуская терминальную программу установленную данным пакетом (например `flit`), вы будете использовать версию из данного виртуального окружения, а не установленную глобально.


### Flit

**FastAPI** использует <a href="https://flit.readthedocs.io/en/latest/index.html" class="external-link" target="_blank">Flit</a> для сборки, упаковки и публикации проекта.

После того как вы активируете виртуальную среду, установите `flit`:

<div class="termy">

```console
$ pip install flit

---> 100%
```

</div>

Теперь повторно активируйте виртуальную среду, чтобы убедиться, что вы используете только что установленный `flit` (а не глобальный).

А теперь используйте `flit` для установки зависимостей:

=== "Linux, macOS"

    <div class="termy">

    ```console
    $ flit install --deps develop --symlink

    ---> 100%
    ```

    </div>

=== "Windows"

    Если вы используете Windows, используйте `--pth-File` вместо `--symlink`:

    <div class="termy">

    ```console
    $ flit install --deps develop --pth-file

    ---> 100%
    ```

    </div>

Он установит все зависимости и ваш локальный FastAPI в вашу локальную среду.

#### Использование локального FastAPI

Если вы создаете файл Python, который импортирует и использует FastAPI, и запускаете его с Python вашей локальной среды, он будет использовать ваш локально установленный FastAPI.

И если вы обновите этот локальный FastAPI, так как он установлен с помощью `--symlink` (или` --pth-file` в Windows), он будет использовать новую версию FastAPI, которую вы только что обновили, когда вы снова запустите этот файл Python.

Таким образом, вам не нужно «устанавливать» локальную версию, чтобы иметь возможность проверять каждое изменение.

### Форматирование

ВЫ можете запустить скрипт который отформатирует и очистит весь ваш код:

<div class="termy">

```console
$ bash scripts/format.sh
```

</div>

Он так же отсортирует ваши import'ы.

Чтобы он мог правильно их отсортировать, вам необходимо, чтобы FastAPI был установлен локально в вашей среде, с помощью команды в разделе выше, используя `--symlink` (или `--pth-file` в Windows).

### Форматирование import'ов

Есть еще один скрипт, который форматирует все импорты и проверяет, нет ли у вас неиспользуемых операций импорта модулей:

<div class="termy">

```console
$ bash scripts/format-imports.sh
```

</div>

Поскольку он запускает одну команду за другой, изменяет и возвращает множество файлов, его выполнение занимает немного больше времени, поэтому может быть проще использовать `scripts/format.sh` почаще и `scripts/format-imports.sh` только перед commit'ом.

## Документация

Во-первых, убедитесь, что вы настроили свою среду, как описано выше, дабы все зависимости были установленны.

В написании документации используется <a href="https://www.mkdocs.org/" class="external-link" target="_blank">MkDocs</a>.

Также есть дополнительные инструменты/скрипты для обработки переводов в `./scripts/docs.py`.

!!! Подсказка
    Вам не нужно смотреть код в `./scripts/docs.py`, вы просто запускаете его из командной строки.

Вся оригинальная документация находится в формате Markdown в каталоге `./docs/en/`.

Многие туториалы содержат блоки код.

В большинстве случаев эти блоки кода представляют собой фактические законченные приложения, которые можно запускать как есть.

Фактически, эти блоки кода не записываются внутри Markdown, они представляют собой файлы Python в каталоге `./docs_src/`.

И эти файлы Python включаются/вводятся в документацию при генерации страницы сайта.

### Документация для тестов

Большинство тестов фактически выполняется на примерах исходных файлов в документации.

Это помогает убедиться что:

* Документация актуальна.
* Примеры документации можно запускать как есть.
* Большинство функций описано в документации, что обеспечивается тестовым покрытием.

Во время локальной разработки есть скрипт, который создает сайт и проверяет наличие изменений, перезагружаясь в реальном времени:

<div class="termy">

```console
$ python ./scripts/docs.py live

<span style="color: green;">[INFO]</span> Serving on http://127.0.0.1:8008
<span style="color: green;">[INFO]</span> Start watching changes
<span style="color: green;">[INFO]</span> Start detecting changes
```

</div>

После этого документация будет отображаться по адресу `http://127.0.0.1:8008`.

Таким образом, вы можете редактировать документацию/исходные файлы и видеть изменения в реальном времени.

#### Typer CLI (по желанию)

Показанные здесь инструкции показывают как использовать скрипт в `./scripts/docs.py` напрямую из `python`

Но вы так же можете использовать <a href="https://typer.tiangolo.com/typer-cli/" class="external-link" target="_blank">Typer CLI</a>, и вы получите автозаполнение команд в вашем терминале после завершения установки.

Если вы уже установили Typer CLI, вы можете установить автозаполнение используя:

<div class="termy">

```console
$ typer --install-completion

zsh completion installed in /home/user/.bashrc.
Completion will take effect once you restart the terminal.
```

</div>

### Запуск приложения и документации одновременно

Если вы запустите примеры:

<div class="termy">

```console
$ uvicorn tutorial001:app --reload

<span style="color: green;">INFO</span>:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
```

</div>

поскольку Uvicorn по умолчанию будет использовать порт `8000`, документация по порту `8008` не будет конфликтовать.

### Переводы

Помощь в переводе документации это БЕСЦЕННО! И это невозможно сделать без помощи сообщества по всему миру. 🌎 🚀

Ниже представлены шаги которые могут помочь с переводом.

#### Рекомендации и примечания

* Check the currently <a href="https://github.com/tiangolo/fastapi/pulls" class="external-link" target="_blank">existing pull requests</a> for your language and add reviews requesting changes or approving them.

!!! tip
    You can <a href="https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/commenting-on-a-pull-request" class="external-link" target="_blank">add comments with change suggestions</a> to existing pull requests.

    Check the docs about <a href="https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-request-reviews" class="external-link" target="_blank">adding a pull request review</a> to approve it or request changes.

* Check in the <a href="https://github.com/tiangolo/fastapi/issues" class="external-link" target="_blank">issues</a> to see if there's one coordinating translations for your language.

* Add a single pull request per page translated. That will make it much easier for others to review it.

For the languages I don't speak, I'll wait for several others to review the translation before merging.

* You can also check if there are translations for your language and add a review to them, that will help me know that the translation is correct and I can merge it.

* Use the same Python examples and only translate the text in the docs. You don't have to change anything for this to work.

* Use the same images, file names, and links. You don't have to change anything for it to work.

* To check the 2-letter code for the language you want to translate you can use the table <a href="https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" class="external-link" target="_blank">List of ISO 639-1 codes</a>.

#### Existing language

Let's say you want to translate a page for a language that already has translations for some pages, like Spanish.

In the case of Spanish, the 2-letter code is `es`. So, the directory for Spanish translations is located at `docs/es/`.

!!! tip
    The main ("official") language is English, located at `docs/en/`.

Now run the live server for the docs in Spanish:

<div class="termy">

```console
// Use the command "live" and pass the language code as a CLI argument
$ python ./scripts/docs.py live es

<span style="color: green;">[INFO]</span> Serving on http://127.0.0.1:8008
<span style="color: green;">[INFO]</span> Start watching changes
<span style="color: green;">[INFO]</span> Start detecting changes
```

</div>

Now you can go to <a href="http://127.0.0.1:8008" class="external-link" target="_blank">http://127.0.0.1:8008</a> and see your changes live.

If you look at the FastAPI docs website, you will see that every language has all the pages. But some pages are not translated and have a notification about the missing translation.

But when you run it locally like this, you will only see the pages that are already translated.

Now let's say that you want to add a translation for the section [Features](features.md){.internal-link target=_blank}.

* Copy the file at:

```
docs/en/docs/features.md
```

* Paste it in exactly the same location but for the language you want to translate, e.g.:

```
docs/es/docs/features.md
```

!!! tip
    Notice that the only change in the path and file name is the language code, from `en` to `es`.

* Now open the MkDocs config file for English at:

```
docs/en/docs/mkdocs.yml
```

* Find the place where that `docs/features.md` is located in the config file. Somewhere like:

```YAML hl_lines="8"
site_name: FastAPI
# More stuff
nav:
- FastAPI: index.md
- Languages:
  - en: /
  - es: /es/
- features.md
```

* Open the MkDocs config file for the language you are editing, e.g.:

```
docs/es/docs/mkdocs.yml
```

* Add it there at the exact same location it was for English, e.g.:

```YAML hl_lines="8"
site_name: FastAPI
# More stuff
nav:
- FastAPI: index.md
- Languages:
  - en: /
  - es: /es/
- features.md
```

Make sure that if there are other entries, the new entry with your translation is exactly in the same order as in the English version.

If you go to your browser you will see that now the docs show your new section. 🎉

Now you can translate it all and see how it looks as you save the file.

#### New Language

Let's say that you want to add translations for a language that is not yet translated, not even some pages.

Let's say you want to add translations for Creole, and it's not yet there in the docs.

Checking the link from above, the code for "Creole" is `ht`.

The next step is to run the script to generate a new translation directory:

<div class="termy">

```console
// Use the command new-lang, pass the language code as a CLI argument
$ python ./scripts/docs.py new-lang ht

Successfully initialized: docs/ht
Updating ht
Updating en
```

</div>

Now you can check in your code editor the newly created directory `docs/ht/`.

!!! tip
    Create a first pull request with just this, to set up the configuration for the new language, before adding translations.

    That way others can help with other pages while you work on the first one. 🚀

Start by translating the main page, `docs/ht/index.md`.

Then you can continue with the previous instructions, for an "Existing Language".

##### New Language not supported

If when running the live server script you get an error about the language not being supported, something like:

```
 raise TemplateNotFound(template)
jinja2.exceptions.TemplateNotFound: partials/language/xx.html
```

That means that the theme doesn't support that language (in this case, with a fake 2-letter code of `xx`).

But don't worry, you can set the theme language to English and then translate the content of the docs.

If you need to do that, edit the `mkdocs.yml` for your new language, it will have something like:

```YAML hl_lines="5"
site_name: FastAPI
# More stuff
theme:
  # More stuff
  language: xx
```

Change that language from `xx` (from your language code) to `en`.

Then you can start the live server again.

#### Preview the result

When you use the script at `./scripts/docs.py` with the `live` command it only shows the files and translations available for the current language.

But once you are done, you can test it all as it would look online.

To do that, first build all the docs:

<div class="termy">

```console
// Use the command "build-all", this will take a bit
$ python ./scripts/docs.py build-all

Updating es
Updating en
Building docs for: en
Building docs for: es
Successfully built docs for: es
Copying en index.md to README.md
```

</div>

That generates all the docs at `./docs_build/` for each language. This includes adding any files with missing translations, with a note saying that "this file doesn't have a translation yet". But you don't have to do anything with that directory.

Then it builds all those independent MkDocs sites for each language, combines them, and generates the final output at `./site/`.

Then you can serve that with the command `serve`:

<div class="termy">

```console
// Use the command "serve" after running "build-all"
$ python ./scripts/docs.py serve

Warning: this is a very simple server. For development, use mkdocs serve instead.
This is here only to preview a site with translations already built.
Make sure you run the build-all command first.
Serving at: http://127.0.0.1:8008
```

</div>

## Tests

There is a script that you can run locally to test all the code and generate coverage reports in HTML:

<div class="termy">

```console
$ bash scripts/test-cov-html.sh
```

</div>

This command generates a directory `./htmlcov/`, if you open the file `./htmlcov/index.html` in your browser, you can explore interactively the regions of code that are covered by the tests, and notice if there is any region missing.
