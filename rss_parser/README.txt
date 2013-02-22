RSS Parser
=======================

From .info description: This is a simple parser for RSS (thinking Twitter here). It creates the class RssParser that can be called in nodes/blocks. The class generates a cached file that gets refreshed if it's older than 60 seconds. 

Example Use (SCRC Twitter feed on library.gwu.edu):

<div style="width:100%;"><div class="twitter-block"><a href="http://twitter.com/gelmanlibrary">Latest from SCRC on Twitter <img alt="Twitter" height="16" src="../sites/all/themes/Libsite7/images/icons/icon-twitter.png" title="Twitter" width="16" /></a></div>
</div>

<div class="twitter-feed">
<?php
  
$parser = new RssParser(); // instantiate the class
$blog_feed = $parser->checkCache(array('scrc-blog' => 'http://api.twitter.com/1/statuses/user_timeline.rss?screen_name=GWUArchives')); // load the RSS
?>

<?php
foreach ($blog_feed as $key => $items)
{
    if ($key < 3): ?>
    <? $tweettext = substr($items['title'], 11) ?>
    <p class="twitter-text"><a href='<?= $items['link'] ?>' title='see the full tweet on Twitter'>@GWUArchives</a>: <?= $tweettext ?></p>
    <?php
    endif;
} //endforeach
?>
</div>

Adapted from Tony Thomas http://anthonygthomas.com/2011/03/12/simple-rss-parsing-and-caching-using-php/