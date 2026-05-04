---
title: '[Docker] 獲取Image的三種方式'
author: Bocky
type: post
date: 2021-07-12T09:12:25+00:00
url: /2021/07/12/docker-獲取image的三種方式/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
<div class="wp-block-group">
  <div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
    <div class="wp-block-group">
      <div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
        <p>
          獲取Image的三種方式:
        </p>
        
        <div class="wp-block-group">
          <div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
            <ol class="wp-block-list">
              <li>
                從Registry取得Image &#8211; <a href="https://docs.docker.com/registry/">registry</a><ul>
                  <li>
                    public（公開的，任何人都可以使用）
                  </li>
                  <li>
                    private（私有）
                  </li>
                </ul>
              </li>
              
              <li>
                文件導入(可離線時使用）
              </li>
              <li>
                從Dockerfile建造
              </li>
            </ol>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

# 從Registry取得Image 

如果沒有提供registry名稱的話，預設是從[DockerHub][1]取得。  
如果不指定的話會下載lates。

<pre class="wp-block-code"><code class="">docker image pull nginx</code></pre>

如果想指定版本的話就加入:tag名稱

<pre class="wp-block-code"><code class="">docker image pull nginx:1.20.1</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Kj3d9t4.png" alt="" /> </figure> 

查看已下載的Image

<pre class="wp-block-code"><code class="">docker image ls</code></pre>

顯示Image的相關訊息

<pre class="wp-block-code"><code class="">docker image inspect IMAGE_ID</code></pre>

刪除Image

如果有容器正在使用，無論是運行中或是關閉狀態，會無法刪除。

<pre class="wp-block-code"><code class="">docker image rm IMAGE_ID</code></pre>

# 文件導入Image 

其他兩種都是要在有網路的狀況下才可以使用，若是電腦沒有網路的話，可以使用導入的方式。

建構Image指令如下:

<pre class="wp-block-code"><code class="">docker image save nginx[:版本] -o 檔案名稱</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/OmxitSX.png" alt="" /> </figure> 

導入Image

<pre class="wp-block-code"><code class="">docker image load -i 檔案路徑</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/ODhSf7a.png" alt="" /> </figure> 

# 從Dockerfile建造 

[Dockerfile參考][2]

將下方兩個檔案存在同一個資料夾：  
檔名：hello.py

<pre class="wp-block-code"><code lang="python" class="language-python">print("Hello this python!")</code></pre>

檔名：dockerfile

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">FROM ubuntu:20.04
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y python3.9 python3-pip python3.9-dev
ADD hello.py /
CMD ["python3", "/hello.py"]</code></pre>

我把這兩個檔案放在名為coding的資料夾裡面。  
<img decoding="async" src="https://i.imgur.com/ZZQiUBP.png" alt="" /> 

接下來從dockerfile建構Image:

<ul class="wp-block-list">
  <li>
    -t :替image命名所需帶入
  </li>
</ul>

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">docker image build -t hello dockerfile路徑
docker image ls # 查看是否有名為hello的image</code></pre>

下圖紅框是我們想要為這個image的命名。  
黃框是dockerfile的路徑。  
<img decoding="async" src="https://i.imgur.com/4EiTOQO.png" alt="" /> 

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker run -it hello</code></pre>

看看有沒有顯示hello.py的字串。  
<img decoding="async" src="https://i.imgur.com/NjapyIi.png" alt="" />

 [1]: https://hub.docker.com/
 [2]: https://docs.docker.com/engine/reference/builder/