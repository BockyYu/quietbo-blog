---
title: '[SQL] REFERENCES 外來鍵的用法(含範例與mysql)'
author: Bocky
type: post
date: 2022-03-01T07:20:41+00:00
url: /2022/03/01/sql-references-外來鍵的用法含範例與mysql/
categories:
  - MySQL
tags:
  - Mysql

---
下方演示: MySQL  
GUI: [tabPlus][1]

在學習SQL時一定會學到外來鍵，外來鍵的目的是**確定資料的參考完整性(referential integrity)**，簡單來說，就是**只有被准許的資料值才會被存入資料庫內**

下方以一個生活例子來舉例:  
1個頻道(電視台)會依據不同時間有不同節目，當然**沒有頻道就不會有節目撥出**，也就是一對多。如下圖:<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/hP9x7EB.png" alt="" /> </figure> 

頻道:

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">CREATE TABLE `channel` (
  `id` int PRIMARY KEY,
  `channel_name` varchar(255) NOT NULL
);</code></pre>

節目:

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">CREATE TABLE `programme` (
  `id` int PRIMARY KEY AUTO_INCREMENT,
  `channel_id` int,
  `programme_name` varchar(255),
  `start_time` datetime DEFAULT (now()),
  `end_time` datetime DEFAULT (now()),
  FOREIGN KEY(channel_id) REFERENCES channel(id)
);</code></pre>

加入資料1:

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">INSERT INTO `channel` (`id`, `channel_name`) VALUES
(7, '恩恩新聞'),
(8, '探索世界'),
(9, '東西購物');</code></pre>

加入資料2:

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">INSERT INTO `programme` (`channel_id`, `programme_name`, `start_time`, `end_time`) VALUES
(7, '3點新聞', '2022-03-01 15:00:00', '2022-03-01 16:00:00'),
(7, '4點新聞', '2022-03-01 16:00:00', '2022-03-01 17:00:00'),
(7, '5點新聞', '2022-03-01 17:00:00', '2022-03-01 18:00:00'),
(8, '說書人', '2022-03-01 15:00:00', '2022-03-01 16:00:00'),
(8, '科學時間', '2022-03-01 16:00:00', '2022-03-01 17:00:00'),
(8, '海底裡', '2022-03-01 17:00:00', '2022-03-01 18:00:00'),
(9, '3點購物時間', '2022-03-01 15:00:00', '2022-03-01 16:00:00'),
(9, '4點購物時間', '2022-03-01 16:00:00', '2022-03-01 17:00:00'),
(9, '5點購物時間', '2022-03-01 17:00:00', '2022-03-01 18:00:00'),</code></pre>

嘗試當加入一筆沒有在channel內的id

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">INSERT INTO `programme` (`channel_id`, `programme_name`, `start_time`, `end_time`) VALUES
(10, '一起出去玩', '2022-03-01 17:00:00', '2022-03-01 18:00:00');</code></pre>

錯誤訊息如下:

<pre class="wp-block-code"><code lang="" class="">Cannot add or update a child row: a foreign key constraint fails (`general`.`programme`, CONSTRAINT `programme_ibfk_1` FOREIGN KEY (`channel_id`) REFERENCES `channel` (`id`))</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/X796Vf2.png" alt="" /> </figure> 

補充

當表已經建立完畢後，設置外來鍵:

<pre class="wp-block-code"><code lang="" class="">ALTER TABLE `programme` ADD FOREIGN KEY (`channel_id`) REFERENCES `channel` (`id`);</code></pre>

可參考:<a rel="noreferrer noopener" href="https://www.fooish.com/sql/foreign-key-constraint.html" data-type="URL" data-id="https://www.fooish.com/sql/foreign-key-constraint.html" target="_blank">fooish</a>

 [1]: https://tableplus.com/