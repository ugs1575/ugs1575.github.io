---
layout: post
title: mac laravel 환경 잡기
---

# mac laravel 환경 잡기

1. home brew 설치
2. php 설치

    ```bash
    brew install php
    ```

3. mysql 설치

    ```bash
    brew install mysql
    ```

    - mysql 실행

    ```bash
    brew services start mysql
    ```

4. composer 설치

5. laravel 설치

```bash
composer global require laravel/installer
```

6. vender path 잡기

```bash
vi ~/.bashrc
```

- 아래 작성 후 저장

```bash
export PATH="$HOME/.composer/vendor/bin:$PATH"
```

- 변경 적용

```bash
source ~/.bashrc
```

1. home brew 설치
2. php 설치

    ```bash
    brew install php
    ```

3. mysql 설치

    ```bash
    brew install mysql
    ```

    - mysql 실행

    ```bash
    brew services start mysql
    ```

4. composer 설치

5. laravel 설치

```bash
composer global require laravel/installer
```

6. vender path 잡기

```bash
vi ~/.bashrc
```

- 아래 작성 후 저장

```bash
export PATH="$HOME/.composer/vendor/bin:$PATH"
```

- 변경 적용

```bash
source ~/.bashrc
```