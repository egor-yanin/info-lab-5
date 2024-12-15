# Отчёт по лабораторной работe 4

## Задание 1

Я создал репозиторий git-practice, в котором выполнял эту лабораторную работу

```bash
echo "# git-practice" >> README.md
git init
git add README.md
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/egor-yanin/git-practice.git
git push -u origin main
```

Также я добавил в репозиторий файл example.txt для проверки на подпись.

```bash
touch example.txt
git add example.txt
git commit -m "Add example.txt"
```

Чтобы проверить наличие подписи в текстовых файлах я написал следующий bash-скрипт:

```bash
#!/bin/bash

SIGNATURE="XD"
FAILED_FILES=()

FILES=$(git diff --cached --name-only | grep '\.txt$')

for FILE in $FILES; do
    if [ -f "$FILE" ]; then
        LAST_LINE=$(tail -n 1 "$FILE")
        if [ "$LAST_LINE" != "$SIGNATURE" ]; then
            FAILED_FILES+=("$FILE")
        fi
    fi
done

if [ ${#FAILED_FILES[@]} -ne 0 ]; then
    echo "Ошибка: Следующие файлы не содержат подпись '$SIGNATURE' в конце:"
    for FILE in "${FAILED_FILES[@]}"; do
        echo "  - $FILE"
    done
    echo "Пожалуйста, добавьте подпись в конец файлов и повторите коммит."
    exit 1
fi

exit 0
```

Он проверяет все файлы .txt, в которых произошли изменения, на наличие подписи в последней строке. Если в каком-то файле нет подписи, коммит не завершится, и будет выведено сообшение об ошибке и указаны файлы, в которых нет подписи.  
Чтобы скрипт автоматически исполнялся при проведении коммита, я поместил его в директорию .git/hooks/ под названием pre-commit

![commit](https://github.com/user-attachments/assets/2a3768ea-1674-45b2-9115-569770deb1e9)

## Задание 2

В этом же репозитории я попрактиковался в использовании Git Flow.
