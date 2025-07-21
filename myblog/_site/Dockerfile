# 使用官方 Ruby 镜像作为基础
FROM ruby:3.2.2-alpine3.18

# 安装构建 native gems 所需的工具和库
# ruby-dev: 包含 Ruby 头文件和开发库
# build-base: 包含 gcc, make 等基础构建工具
# libxml2-dev, libxslt-dev: 如果您的 Gemfile 中有依赖于 XML/XSLT 的 gem（例如 nokogiri），则需要
# zlib-dev: 压缩库，一些 gem 可能需要
# openssl-dev: SSL/TLS 库，很多网络相关的 gem 需要
RUN apk add --no-cache \
    build-base \
    ruby-dev \
    zlib-dev \
    libxml2-dev \
    libxslt-dev \
    openssl-dev

# 设置工作目录
WORKDIR /usr/src/app

# 复制 Gemfile 和 Gemfile.lock，并安装依赖
COPY Gemfile Gemfile.lock ./
RUN bundle install --jobs 4 --retry 3

# 复制整个项目到容器中
COPY . .

# 暴露 Jekyll 的默认端口
EXPOSE 4000

# 启动 Jekyll 服务器
CMD ["bundle", "exec", "jekyll", "serve", "--host", "0.0.0.0"]