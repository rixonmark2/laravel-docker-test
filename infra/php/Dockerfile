FROM php:8.0-fpm-buster
# ◆FROM
# ・ベースイメージを設定するための命令
# ・「FROM イメージ名:タグ名」という風に指定
#
# ◆PHP-FPM
# ・「FastCGI Process Manager」の略
# ・PHP5.4.0から公式サポートされた、PHP標準のアプリケーションサーバ
# ・FastCGIというプロトコルで通信するよう実装されている
#
# ◆FastCGI
# ・「処理の高速化」「負荷の軽減」をしたCGI
# ・一度、起動したらしばらく終了しない仕組み
# ・そのため、処理が連続する場合の効率化が出来る
#
# ◆CGI
# ・「Common Gateway Interface」の略
# ・クライアントの要求に応じて、Webサーバ上のプログラムを動かし、実行結果をクライアントに返す仕組み
#
# ◆buster
# ・「Debian 10.0」のコードネーム
#
# ◆参考文献
# ・PHP-FPMとは...https://www.bnote.net/centos/php-fpm_on_nginx.html
# ・FastCGIとは...https://wa3.i-3-i.info/word12806.html
# ・CGIとは...https://www.infraexpert.com/study/tcpip16.5.html
# ・busterとは...https://ja.wikipedia.org/wiki/Debian


SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]
# ◆SHELL
# ・デフォルトのシェルを上書きするための命令
# ・「SHELL ["hoge", "-huga", "-piyo"]」で「hoge -huga -piyo」のように実行される
#
# ◆シェル
# ・人の入力をコンピュータに伝えるプログラム
#
# ◆/bin/bash
# ・UNIX系のOS（Linuxとか）で使われるシェル「bash」の本体ファイル
#
# ◆-o
# ・シェルオプションを有効にするオプション
#
# ◆-e
# ・シェルスクリプト内で何らかのエラーが発生した時点で、それ以降の処理を中断するオプション
#
# ◆-u
# ・未定義の変数に対して読み込み等を行おうとした際にエラーにするオプション
#
# ◆-x
# ・シェルスクリプト内で実際に実行されたコマンドを表示するオプション
#
# ◆pipefail
# ・パイプを使用した処理の中でエラーが起きた際に処理を止めるオプション
#
# ◆-c
# ・文字列を渡すことで、文字列をコマンドとして実行させることが出来る
#
# ◆参考文献
# ・シェルとは...https://wa3.i-3-i.info/word11219.html
# ・/bin/bashとは...https://wa3.i-3-i.info/word14414.html
# ・-oとは...https://www.atmarkit.co.jp/ait/articles/1805/10/news023.html
# ・-xとは...https://shellscript.sunone.me/debug.html
# ・pipefailとは...https://eichisanden.hateblo.jp/entry/2018/01/23/112255
# ・-cとは...https://genzouw.com/entry/2021/01/08/202800/2109/#


ENV COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer
# ◆ENV
# ・環境変数に値を設定するため命令
# ・「ENV key=value」で環境変数keyに値valueを設定
#
# ◆\
# ・改行
# ・可読性の向上
#
# ◆参考文献
# ・ENVとは...https://matsuand.github.io/docs.docker.jp.onthefly/engine/reference/builder/#env
# ・\とは...https://qiita.com/tera_shin/items/efde65d2f875c5d8592a


COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer
# ◆COPY
# ・ローカルファイルをコンテナの中にコピーするための命令
# ・「COPY hoge huga」でローカルファイルhogeを、コンテナ内のhugaにコピーする
#
# ◆--from
# ・別のイメージのファイルを指定するオプション（マルチステージビルド）
# ・「COPY --from=hoge huga piyo」でhogeイメージのhugaファイルをコンテナ内のpiyoにコピーする
#
# ◆参考文献
# ・COPYとは...https://docs.docker.jp/engine/userguide/eng-image/dockerfile_best-practice.html#add-copy


RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
    apt-get install -y nodejs
# ◆RUN
# ・現在のイメージ上で指定したコマンドを実行するための命令
#
# ◆&&
# ・命令コマンドが増えると、その分レイヤが増える
# ・レイヤが増えるとDockerイメージのサイズも大きくなる
# ・そのため、&&を使用し、コマンドをまとめる
#
# ◆apt-get
# ・Debian系のパッケージ管理ツール
#
# ◆apt-get -y install ×××
# ・パッケージのインストール
# ・Laravelに使用するパッケージのみをインストール
#
# ◆参考文献
# ・&&とは...https://www.tohoho-web.com/docker/dockerfile.html


RUN apt-get update && \
    apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-install intl pdo_mysql zip bcmath
# ◆apt-get update
# ・インストール可能なパッケージ一覧を更新する
#
# ◆apt-get clean && rm -rf /var/lib/apt/lists/*
# ・パッケージインストールで使用したキャッシュファイルを削除
#
# ◆docker-php-ext-install intl pdo_mysql zip bcmath
# ・docker-php-ext-installはPHPの公式Dokcerイメージが用意している、PHP拡張ライブラリを簡単に利用するためのコマンド
# ・PHPの拡張ライブラリをインストール


COPY ./php.ini /usr/local/etc/php/php.ini
# ◆COPY
# ・ローカルファイルをコンテナの中にコピーするための命令
# ・「COPY hoge huga」でローカルファイルhogeを、コンテナ内のhugaにコピーする
#
# ◆php.ini
# ・PHPの設定ファイル


WORKDIR /work
# ◆WORKDIR
# ・ワークディレクトリを指定するための命令