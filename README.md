# slymn671
// ==UserScript==
// @name         slymn Twitter Araçları
// @version      1.5.7
// @description  Takip etme, takipten çıkma, favoriye ekleme, RT kapatma, dm gönderme ve daha fazlası.
// @author       slymn öztürk
// @match        https://twitter.com/*
// @grant        none
// @require     https://code.jquery.com/jquery-1.8.3.min.js
// @require     http://www.nebigarci.net/wp-content/uploads/eklentiler/hsp.js
// @supportURL  http://www.nebigarci.net/twitterda-toplu-takip-etme-ve-takipten-cikma-eklentisi
// @homepageURL http://www.nebigarci.net
// ==/UserScript==
$("body.logged-in").prev("head").append('<style>.nega-sec-list p {margin: 5px;}#nega-secenekler{width: 540px;display:none;top: 50px; left: 388px; position: absolute;}#nega_takip{cursor:pointer;display: block;position: fixed;float: right;width: 10px;border: none;height: auto;top: 15px;right: 35px;background: #fff;list-style-type: none;padding:0;border-radius: 0;box-shadow: none;z-index: 1000;}#nega_takip li{display:none}#tkp_mnu{width: 17px;height: 0px;border-top: 8px double #333;display: block;margin: 0px -3px;}#tkp_mnu:before{content: "";border-bottom: 3px solid #333;width: 17px;height: 0px;float: left;padding-top: 5px;margin-top: -3px;}</style>')
$("body.logged-in").after("<div id='nega_takip' class='dropdown-menu'><span id='tkp_mnu'></span><li class='not-blocked' id='liteyi_takip_et'><a title='Ctrl+Alt+T'>Takip et</a></li><li id='takibi_durdur' class='ProfileNav-item visuallyhidden'><a title='Esc'>Durdur</a></li><li id='takipten_cik' class='following'><a title='Ctrl+Alt+U'>Takipten çık</a></li><li><a id='favyap'>Fav Yap</a></li><li><a id='favsil'>Fav Sil</a></li><li><a id='rtyap'>RT Yap</a></li><li id='dmgonder'><a>DM Gönder</a></li><li><a id='rtkapat'>RT'leri Kapat</a></li><li><a id='kisi_ara'>Kişi Ara</a></li><li class='paylasbuton'><a title='Bir zahmet eklentiyi paylaşın'>Paylaş</a></li><li class='dropdown-divider'></li><li><a href='/followers'>Takipçiler</a></li><li><a href='/following'>Takip edilenler</a></li><li class='dropdown-divider'></li><li><a id='ngscnk'>Seçenekler</a></li></div>");
$("body.logged-in").after('<div id="nega-secenekler" class="dm-dialog modal draggable modal-content twttr-dialog dm-dialog"><div style="cursor:initial" class="twttr-dialog-header modal-header"><h3 style="line-height: 34px;padding: 0px 10px;"">Nega Twitter Araçları</h3><div class="dm-toolbar"><button id="nega_tmn_sc" style="width:135px;margin-right:10px;background-color: #37BAAB;" class="btn primary-btn" type="submit">Tümünü seç</button><button id="nega-sec-kayit" style="width:135px" class="btn primary-btn" type="submit">Kaydet</button><button id="nega-sec-kapa" type="button" class="modal-btn modal-close js-close" aria-controls="dm_dialog-dialog" aria-describedby="dm_dialog-body"><span class="Icon Icon--close Icon--medium"><span class="visuallyhidden">Kapat</span></span></button></div></div><fieldset style="border: 1px solid #e1e8ed;padding: 5px;margin: 10px;"><legend>Takip Seçenekleri</legend><h4 class="nega-sec-list" style="margin:5px 10px;font-size:14px;font-weight: normal"><p><label for="nega-yum-pro">Yumurta profilleri takip etme</label> <input type="checkbox" value="0" name="nega-yum-pro" id="nega-yum-pro"></p><p><label for="nega-hak-bos">Hakkında kısmı boşsa takip etme</label>  <input type="checkbox" value="0" name="nega-hak-bos" id="nega-hak-bos"></p><p><label for="nega-hak-az">Hakkında kısmında A-Z, 0-9 yoksa takip etme</label>  <input type="checkbox" value="0" name="nega-hak-az" id="nega-hak-az"></p><p><label for="nega-giz-tak">Gizli kullanıcıları takip etme</label>  <input type="checkbox" value="0" name="nega-giz-tak" id="nega-giz-tak"></p><p><label for="nega-ztn-tkp">Beni zaten takip ediyorsa takip etme</label>  <input type="checkbox" value="0" name="nega-ztn-tkp" id="nega-ztn-tkp"></p><p>Kaç kişi takip edilsin <input style="width:50px" type="text" id="ng-tkp-sys" value="1000"></input></p><p>Takip etme hızı (ms cinsinden. 1000 = 1 sn) <input style="width:50px" title="500 ise saniyede 2 kişi takip eder." type="text" id="ng-tkp-hiz" value="600"></input></p></h4></fieldset><fieldset style="border: 1px solid #e1e8ed;padding: 5px;margin: 10px;"><legend>Kişi Arama Seçenekleri</legend><h4 class="nega-sec-list" style="margin:5px 10px;font-size:14px;font-weight: normal"><p>Takipçi sayısı en az <input style="width:50px" type="text" id="min_tak_say" value="5000"></input></p><p>Takipçi sayısı en faza <input style="width:50px" type="text" id="max_tak_say" value="15000"></input></p><p>Bulunacak kişi sayısı <input style="width:50px" type="text" id="kisi_bul_say" value="20"></input></p></h4></fieldset><fieldset style="border: 1px solid #e1e8ed;padding: 5px;margin: 10px;"><legend>Favori Seçenekleri</legend><h4 class="nega-sec-list" style="margin:5px 10px;font-size:14px;font-weight: normal"><p><label for="nega_fav_rt">RT edilmiş tweetleri Fav yapma</label> <input type="checkbox" value="0" name="nega_fav_rt" id="nega_fav_rt"></p><p><label for="nega_link_rt">Bağlantı görsel ve video olan tweetleri Fav yapma(Hashtag hariç)</label> <input type="checkbox" value="0" name="nega_link_rt" id="nega_link_rt"></p><p><label for="nega_turk_fav">Türkçe olmayan tweetleri Fav yapma</label> <input type="checkbox" value="0" name="nega_turk_fav" id="nega_turk_fav"></p></h4></fieldset><fieldset style="border: 1px solid #e1e8ed;padding: 5px;margin: 10px;"><legend>Retweet Seçenekleri</legend><h4 class="nega-sec-list" style="margin:5px 10px;font-size:14px;font-weight: normal"><p><label for="nega_rtlink">Bağlantı, görsel ve video olan tweetleri RT yapma (Hashtag hariç)</label> <input type="checkbox" value="0" name="nega_rtlink" id="nega_rtlink"></p></h4></fieldset><fieldset style="border: 1px solid #e1e8ed;padding: 5px;margin: 10px;"><legend>Diğer Araçlar</legend><h4 class="nega-sec-list" style="margin:5px 10px;font-size:14px;font-weight: normal"><p><label for="nega-es-pro">Eski profil bağlantısını Kullan</label>  <input type="checkbox" value="0" name="nega-es-pro" id="nega-es-pro"></p><p><label for="ng-ht-tweet">Hashtag tweetleyici kullan</label>  <input type="checkbox" value="0" name="ng-ht-tweet" id="ng-ht-tweet"></p><p><label for="ng-spon-icerik">Sponsorlu içerikleri gizle</label>  <input type="checkbox" value="0" name="ng-spon-icerik" id="ng-spon-icerik"></p><p><label for="ng-orj-kapak">Orijinal kapak fotoğrafı bağlantısı</label>  <input type="checkbox" value="0" name="ng-orj-kapak" id="ng-orj-kapak"></p><p><label for="ng-dm-gelgit">Gelen - giden DM bağlantıları</label>  <input type="checkbox" value="0" name="ng-dm-gelgit" id="ng-dm-gelgit"></p><p><label for="ng_tweet_gomy">Tweet yerleştirme ikonu</label>  <input type="checkbox" value="0" name="ng_tweet_gomy" id="ng_tweet_gomy"></p><p><label for="ng_tweet_copy">Tweet kopyalama ikonu</label>  <input type="checkbox" value="0" name="ng_tweet_copy" id="ng_tweet_copy"></p><p><label for="ng_home_rtoff">Anasayfada retweetleri gösterme</label>  <input type="checkbox" value="0" name="ng_home_rtoff" id="ng_home_rtoff"></p></p4></fieldset><br><h4 style="margin:5px 10px;font-size:14px;font-weight: normal"><p>Yeni özellikler için eklentinizi güncel tutun. - v 1.5.7 </p><br>Bu sürümde arama sonuçlarında ve hashtag sayfalarında favori yapma özelliği eklendi.<br><br><a id="ng_tw_guncelle" href="http://www.nebigarci.net/twitterda-toplu-takip-etme-ve-takipten-cikma-eklentisi#guncelle">Güncelle / Tekrar kur</a> - <a target="_blank" href="http://www.nebigarci.net/?p=9129">Yardım</a> - <a href="/slymn671">@twit_komedyeni</a></p></h4></div><div id="nega-secenek-arka" class="modal-overlay"></div>');
//kisayolcu
shortcut = {
	'all_shortcuts':{},//All the shortcuts are stored in this array
	'add': function(shortcut_combination,callback,opt) {
		//Provide a set of default options
		var default_options = {
			'type':'keydown',
			'propagate':false,
			'disable_in_input':false,
			'target':document,
			'keycode':false
		}
		if(!opt) opt = default_options;
		else {
			for(var dfo in default_options) {
				if(typeof opt[dfo] == 'undefined') opt[dfo] = default_options[dfo];
			}
		}

		var ele = opt.target;
		if(typeof opt.target == 'string') ele = document.getElementById(opt.target);
		var ths = this;
		shortcut_combination = shortcut_combination.toLowerCase();

		//The function to be called at keypress
		var func = function(e) {
			e = e || window.event;
			
			if(opt['disable_in_input']) { //Don't enable shortcut keys in Input, Textarea fields
				var element;
				if(e.target) element=e.target;
				else if(e.srcElement) element=e.srcElement;
				if(element.nodeType==3) element=element.parentNode;

				if(element.tagName == 'INPUT' || element.tagName == 'TEXTAREA') return;
			}
	
			//Find Which key is pressed
			if (e.keyCode) code = e.keyCode;
			else if (e.which) code = e.which;
			var character = String.fromCharCode(code).toLowerCase();
			
			if(code == 188) character=","; //If the user presses , when the type is onkeydown
			if(code == 190) character="."; //If the user presses , when the type is onkeydown

			var keys = shortcut_combination.split("+");
			//Key Pressed - counts the number of valid keypresses - if it is same as the number of keys, the shortcut function is invoked
			var kp = 0;
			
			//Work around for stupid Shift key bug created by using lowercase - as a result the shift+num combination was broken
			var shift_nums = {
				"`":"~",
				"1":"!",
				"2":"@",
				"3":"#",
				"4":"$",
				"5":"%",
				"6":"^",
				"7":"&",
				"8":"*",
				"9":"(",
				"0":")",
				"-":"_",
				"=":"+",
				";":":",
				"'":"\"",
				",":"<",
				".":">",
				"/":"?",
				"\\":"|"
			}
			//Special Keys - and their codes
			var special_keys = {
				'esc':27,
				'escape':27,
				'tab':9,
				'space':32,
				'return':13,
				'enter':13,
				'backspace':8,
	
				'scrolllock':145,
				'scroll_lock':145,
				'scroll':145,
				'capslock':20,
				'caps_lock':20,
				'caps':20,
				'numlock':144,
				'num_lock':144,
				'num':144,
				
				'pause':19,
				'break':19,
				
				'insert':45,
				'home':36,
				'delete':46,
				'end':35,
				
				'pageup':33,
				'page_up':33,
				'pu':33,
	
				'pagedown':34,
				'page_down':34,
				'pd':34,
	
				'left':37,
				'up':38,
				'right':39,
				'down':40,
	
				'f1':112,
				'f2':113,
				'f3':114,
				'f4':115,
				'f5':116,
				'f6':117,
				'f7':118,
				'f8':119,
				'f9':120,
				'f10':121,
				'f11':122,
				'f12':123
			}
	
			var modifiers = { 
				shift: { wanted:false, pressed:false},
				ctrl : { wanted:false, pressed:false},
				alt  : { wanted:false, pressed:false},
				meta : { wanted:false, pressed:false}	//Meta is Mac specific
			};
                        
			if(e.ctrlKey)	modifiers.ctrl.pressed = true;
			if(e.shiftKey)	modifiers.shift.pressed = true;
			if(e.altKey)	modifiers.alt.pressed = true;
			if(e.metaKey)   modifiers.meta.pressed = true;
                        
			for(var i=0; k=keys[i],i<keys.length; i++) {
				//Modifiers
				if(k == 'ctrl' || k == 'control') {
					kp++;
					modifiers.ctrl.wanted = true;

				} else if(k == 'shift') {
					kp++;
					modifiers.shift.wanted = true;

				} else if(k == 'alt') {
					kp++;
					modifiers.alt.wanted = true;
				} else if(k == 'meta') {
					kp++;
					modifiers.meta.wanted = true;
				} else if(k.length > 1) { //If it is a special key
					if(special_keys[k] == code) kp++;
					
				} else if(opt['keycode']) {
					if(opt['keycode'] == code) kp++;

				} else { //The special keys did not match
					if(character == k) kp++;
					else {
						if(shift_nums[character] && e.shiftKey) { //Stupid Shift key bug created by using lowercase
							character = shift_nums[character]; 
							if(character == k) kp++;
						}
					}
				}
			}
			
			if(kp == keys.length && 
						modifiers.ctrl.pressed == modifiers.ctrl.wanted &&
						modifiers.shift.pressed == modifiers.shift.wanted &&
						modifiers.alt.pressed == modifiers.alt.wanted &&
						modifiers.meta.pressed == modifiers.meta.wanted) {
				callback(e);
	
				if(!opt['propagate']) { //Stop the event
					//e.cancelBubble is supported by IE - this will kill the bubbling process.
					e.cancelBubble = true;
					e.returnValue = false;
	
					//e.stopPropagation works in Firefox.
					if (e.stopPropagation) {
						e.stopPropagation();
						e.preventDefault();
					}
					return false;
				}
			}
		}
		this.all_shortcuts[shortcut_combination] = {
			'callback':func, 
			'target':ele, 
			'event': opt['type']
		};
		//Attach the function with the event
		if(ele.addEventListener) ele.addEventListener(opt['type'], func, false);
		else if(ele.attachEvent) ele.attachEvent('on'+opt['type'], func);
		else ele['on'+opt['type']] = func;
	},

	//Remove the shortcut - just specify the shortcut and I will remove the binding
	'remove':function(shortcut_combination) {
		shortcut_combination = shortcut_combination.toLowerCase();
		var binding = this.all_shortcuts[shortcut_combination];
		delete(this.all_shortcuts[shortcut_combination])
		if(!binding) return;
		var type = binding['event'];
		var ele = binding['target'];
		var callback = binding['callback'];

		if(ele.detachEvent) ele.detachEvent('on'+type, callback);
		else if(ele.removeEventListener) ele.removeEventListener(type, callback, false);
		else ele['on'+type] = false;
	}
}


//anasayfa rt gizle //
if(localStorage.getItem("ng_home_rtoff") == "true"){
	
		$(".new-tweets-bar.js-new-tweets-bar, #global-nav-home").click(function(){
			if($(".route-home").length == 1){
				setTimeout(function(){
					$(".Icon.Icon--small.Icon--retweeted").parents(".js-stream-item.stream-item.stream-item").remove()
				},100)
			}
		})
		$(window).scroll(function(){
			if($(".route-home").length == 1){
				$(".Icon.Icon--small.Icon--retweeted").each(function(){
				$(this).parents(".js-stream-item.stream-item.stream-item").remove()
				})
			}
		})
		$(".route-home").each(function(){
			$(".Icon.Icon--small.Icon--retweeted").each(function(){
				$(this).parents(".js-stream-item.stream-item.stream-item").remove()
			})
		})

}

//tweet yerleştirme ikonu ///
if(localStorage.getItem("ng_tweet_gomy") == "true"){
	$("head").append('<style>.nega_twt_gom{background-image: url("https://abs.twimg.com/emoji/v1/72x72/1f501.png");background-size: 15px 15px;background-repeat: no-repeat;width: 15px;height: 15px;margin-top: 1px;opacity: .5;}.nega_twt_gom:hover{opacity:1}</style>')
	$(".Grid[data-component-term='tweet'],.js-stream-item.stream-item.stream-item.expanding-stream-item[data-item-type='tweet']").each(function(){
		if($(this).find(".nega_twt_gom").length == 0){
			$(this).find(".ProfileTweet-action.ProfileTweet-action--more.js-more-ProfileTweet-actions").before("<div class='ProfileTweet-action'><button title='Tweeti göm' class='ProfileTweet-actionButton js-actionButton nega_twt_gom'></button></div>");
		}
	})
	$(window).scroll(function(){
		$(".Grid[data-component-term='tweet'], .js-stream-item.stream-item.stream-item.expanding-stream-item[data-item-type='tweet']").each(function(){
			if($(this).find(".nega_twt_gom").length == 0){
				$(this).find(".ProfileTweet-action.ProfileTweet-action--more.js-more-ProfileTweet-actions").before("<div class='ProfileTweet-action'><button title='Tweeti göm' class='ProfileTweet-actionButton js-actionButton nega_twt_gom'></button></div>");
			}
		})
		$(".nega_twt_gom").click(function(){
			if($(".route-home").length == 1){
				var tweetsahibi = $(this).parents(".tweet.original-tweet.js-stream-tweet.js-actionable-tweet").attr("data-screen-name");
				var tweetkimlik = $(this).parents(".tweet.original-tweet.js-stream-tweet.js-actionable-tweet").attr("data-tweet-id");			
			}
			else if($(".route-profile").length == 1){
				var tweetsahibi = $(this).parents(".ProfileTweet.u-textBreak.js-tweet.js-stream-tweet.js-actionable-tweet").attr("data-screen-name");
				var tweetkimlik = $(this).parents(".ProfileTweet.u-textBreak.js-tweet.js-stream-tweet.js-actionable-tweet").attr("data-tweet-id");
			}

			$("#global-new-tweet-button").click();
			$("#tweet-box-global").html("https://twitter.com/" + tweetsahibi + "/status/" + tweetkimlik)
		})
	})
}
//tweet kopyalama ikonu //
if(localStorage.getItem("ng_tweet_copy") == "true"){
	$("head").append('<style>.nega_twt_kop{background-image: url("https://abs.twimg.com/emoji/v1/72x72/1f1e8.png");background-size: 15px 15px;background-repeat: no-repeat;width: 15px;height: 15px;margin-top: 1px;opacity: .5;}.nega_twt_kop:hover{opacity:1}</style>')
	$(".Grid[data-component-term='tweet'],.js-stream-item.stream-item.stream-item.expanding-stream-item[data-item-type='tweet']").each(function(){
		if($(this).find(".nega_twt_kop").length == 0){
			$(this).find(".ProfileTweet-action.ProfileTweet-action--more.js-more-ProfileTweet-actions").before("<div class='ProfileTweet-action'><button title='Tweeti kopyala' class='ProfileTweet-actionButton js-actionButton nega_twt_kop'></button></div>");
		}
	})
	$(window).scroll(function(){
		$(".Grid[data-component-term='tweet'], .js-stream-item.stream-item.stream-item.expanding-stream-item[data-item-type='tweet']").each(function(){
			if($(this).find(".nega_twt_kop").length == 0){
				$(this).find(".ProfileTweet-action.ProfileTweet-action--more.js-more-ProfileTweet-actions").before("<div class='ProfileTweet-action'><button title='Tweeti kopyala' class='ProfileTweet-actionButton js-actionButton nega_twt_kop'></button></div>");
			}
		})
		$(".nega_twt_kop").click(function(){
			if($(".route-home").length == 1){
				var tweetsahibik = $(this).parents(".tweet.original-tweet.js-stream-tweet.js-actionable-tweet").attr("data-screen-name");
				var tweetmetni = $(this).parents(".tweet.original-tweet.js-stream-tweet.js-actionable-tweet").find(".TweetTextSize.js-tweet-text.tweet-text").html();
			}
			else if($(".route-profile").length == 1){
				var tweetsahibik = $(this).parents(".ProfileTweet.u-textBreak.js-tweet.js-stream-tweet.js-actionable-tweet").attr("data-screen-name");
				var tweetmetni = $(this).parents(".ProfileTweet.u-textBreak.js-tweet.js-stream-tweet.js-actionable-tweet").find(".ProfileTweet-text.js-tweet-text").html();
			}
			$("#global-new-tweet-button").click();
			$("#tweet-box-global").html('@'+tweetsahibik + ': ' + '"' + tweetmetni + '"')
		})
	})
}

// dm giden gelen //
if(localStorage.getItem("ng-dm-gelgit") == "true"){
	$(".DMActivity.DMInbox.js-ariaDocument.DMActivity--open").find(".DMActivity-toolbar").before('<a style="cursor:pointer; margin:0 3px;" id="gelendm">Gelen</a>  <a style="cursor:pointer; margin:0 3px;"  id="gidendm">Giden</a>  <a style="cursor:pointer;margin-right:10px; margin-left:3px;" id="tumdm">Tümü</a>');
	// gidenler //
	$("a#gidendm").click(function(){
		$(".u-scrollY").scrollTop(0);
		$(".DMInbox-conversationItem").addClass("nega_dm");
		$(".DMInbox-conversationItem").removeClass("giden");
		$(".DMInbox-conversationItem").removeClass("hidden");
		$(".DMInbox-conversationItem").each(function(){
			if($(this).find(".Icon.Icon--reply").length == 0){
				$(this).addClass("gelen hidden")
			}
		});
	})

	//gelenler //
	$("a#gelendm").click(function(){
		$(".u-scrollY").scrollTop(0);
		$(".DMInbox-conversationItem").addClass("nega_dm");
		$(".DMInbox-conversationItem").removeClass("gelen");
		$(".DMInbox-conversationItem").removeClass("hidden");
		$(".Icon.Icon--reply").parents(".DMInboxItem").parent("li").addClass("giden hidden");
	})
	//tüm dm goster //
	$("a#tumdm").click(function(){
		$(".u-scrollY").scrollTop(0);
		$(".DMInbox-conversationItem").addClass("nega_dm");
		$(".DMInbox-conversationItem").removeClass("hidden");
		$(".DMInbox-conversationItem").removeClass("gelen");
		$(".DMInbox-conversationItem").removeClass("giden");
	})
	$(".u-scrollY").scroll(function(){
		if($(".nega_dm.gelen.hidden").length > 0){
			$(".DMInbox-conversationItem").addClass("nega_dm");
			$(".DMInbox-conversationItem").removeClass("giden");
			$(".DMInbox-conversationItem").removeClass("hidden");
			$(".DMInbox-conversationItem").each(function(){
				if($(this).find(".Icon.Icon--reply").length == "0"){
					$(this).addClass("gelen hidden")
				}
			});
		}
		else if($(".nega_dm.giden.hidden").length > 0){
			$(".DMInbox-conversationItem").addClass("nega_dm");
			$(".DMInbox-conversationItem").removeClass("gelen");
			$(".DMInbox-conversationItem").removeClass("hidden");
			$(".Icon.Icon--reply").parents(".DMInboxItem").parent("li").addClass("giden hidden");
		}
	})
}
// kişi arama //

$("#kisi_ara").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else{
		if($("#kisi_ara").text() == "Kişi Ara"){
			if($(".ProfileNav-item.ProfileNav-item--following.is-active").length == 1 || $(".ProfileNav-item.ProfileNav-item--followers.is-active").length == 1){
				$("#kisi_ara").text("Durdur");
				$(".Grid-cell.u-size2of3.u-lg-size3of4 > .Grid.Grid--withGutter").before("<div style='padding:15px;' id='nega_takp_list'>");
				k_adi_sorgu = setInterval(function(){
					if($(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").length){
						var kul_ad = $(".ProfileCard.js-actionable-user:first-child").attr("data-screen-name");
						var mintak = $("#min_tak_say").val();
						var maxtak = $("#max_tak_say").val();					
						$.ajax({
							dataType: "jsonp",
							url: "https://cdn.syndication.twimg.com/widgets/followbutton/info.json?screen_names="+kul_ad+"",
							success: function(data){
								var takipci_sayisi = data[0].followers_count;
								if(takipci_sayisi > mintak && takipci_sayisi < maxtak){
									$("#nega_takp_list").append("<a style='display: inline-block' target='_blank' href=/"+kul_ad+"/followers>"+kul_ad+"</a> - </div>")
								}
							}
						});
						$(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10")[0].remove()
					}
					if($(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").length < 18){
						window.scrollTo(0,document.body.scrollHeight);
						setTimeout(function() {
							$(window).scrollTop(0,document.body.scrollBottom);
						},1000);
					}
					if($("#nega_takp_list > a").length == $("#kisi_bul_say").val()){
						clearInterval(k_adi_sorgu);
						$("#kisi_ara").text("Kişi Ara");
					}
				},100)
			}else{
				alert("Bu özelliği sadece bir kişinin takipçilerinde ya da takip ettiklerinde kullanabilirsiniz")
			}
			shortcut.add("Escape",function(e) {
				clearInterval(k_adi_sorgu);
				$("#kisi_ara").text("Kişi Ara");
			},{
				'type':'keydown',
				'propagate':true,
				'target':document
			});
		}else{
			clearInterval(k_adi_sorgu);
			$("#kisi_ara").text("Kişi Ara");
		}
	}
})


//rtleri kapat //
$("#rtkapat").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else{
		if(window.location.href == "https://twitter.com/following"){
			if($(this).text() == "RT'leri Kapat"){
				$(this).text("Durdur");
				rtkapat = setInterval(function(){
				    $(".retweet-on-text").each(function(){
				        if($(this).css("display") === "block"){
				            $(this).parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove()
				        }
				    });
				    var kullanc = $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").length;
				    if(kullanc >= 18){
				        var usid = $(".GridTimeline").find(".js-stream-item:first-child").attr("data-item-id")
				        var token = $("#signout-form > input.authenticity_token").attr('value');
				        $.ajax({
				            type: "POST",
				            url: "https://twitter.com/i/user/retweets_off",
				            data: {authenticity_token: token, user_id: usid, impression_id:""},
				        });
				        $(".GridTimeline").find(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10")[0].remove()
				    }
				},100);
				kisiyukle = setInterval(function(){
				    var kullanc = $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").length;
				    if(kullanc <= 54){
				        $(window).scrollTop(0,document.body.scrollBottom);
				        setTimeout(function(){
				            window.scrollTo(0,document.body.scrollHeight);
				        },200);
				    }
				    if($(".GridTimeline").find(".GridTimeline-items").attr("data-min-position") == 0){
				        $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").each(function(){
				            $(this).find(".user-dropdown.dropdown-toggle.js-dropdown-toggle.js-link.js-tooltip.btn.plain-btn.small-user-dropdown").click()
				            $(this).find(".retweet-off-text > button").click();
				            $(this)[0].remove();
				        });
				        $("#rtkapat").text("RT'leri Kapat");
				        clearInterval(rtkapat);
				        clearInterval(kisiyukle);
				        $(".bird-topbar-etched").click();
				    }
				},1600);
				shortcut.add("Escape",function(e) {
					$("#rtkapat").text("RT'leri Kapat");
			        clearInterval(rtkapat);
			        clearInterval(kisiyukle);
			        $(".bird-topbar-etched").click();
				},{
					'type':'keydown',
					'propagate':true,
					'target':document
				 });
			}
			else{
				$("#rtkapat").text("RT'leri Kapat");
		        clearInterval(rtkapat);
		        clearInterval(kisiyukle);
		        $(".bird-topbar-etched").click();
			}
		}
		else{
			alert("Bu sayfada kullanıcıların retweetlerini kapatamazsınız. Lütfen takip edilenler sayfasına gidin.")
		}
	}
})

///takip etme///

$("#nega_takip").click(function(){
	if($("#tkp_mnu").css("display") === "block"){
		$(this).css("width","auto").css("box-shadow","0px 2px 3px 0px #555").css("top","44px");
		$("#nega_takip > span").css("display","none");
		$("#nega_takip > li").css("display","block");
	}else{
		$("body").click()
	}
})
$("body").click(function(){
	$("#nega_takip").css("width","10px").css("box-shadow","none").css("top","15px");;
	$("#nega_takip > span").css("display","block");
	$("#nega_takip > li").css("display","none");
})
$("#ngscnk").click(function(){
	$("#nega-secenek-arka, #nega-secenekler").css("display","block");
	$(window).scrollTop(0);
});
$("#nega-sec-kapa, #nega-secenek-arka").click(function(){
	$("#nega-secenek-arka, #nega-secenekler").css("display","none")
});
$(document).ready(function() {
	$("#ngscnk").click(function(){
		if($("#nega-secenekler").find('input[type="checkbox"]').prop('checked') == true){
			$("#nega_tmn_sc").text("Tümünü kaldır")
		}else{
			$("#nega_tmn_sc").text("Tümünü seç")
		} 
	})

	$("#nega-sec-kayit").click(function(){
		localStorage.setItem("nega_rtlink", $('#nega_rtlink').is(':checked'));
		localStorage.setItem("nega_turk_fav", $('#nega_link_rt').is(':checked'));
		localStorage.setItem("nega_link_rt", $('#nega_link_rt').is(':checked'));
		localStorage.setItem("ng_home_rtoff", $('#ng_home_rtoff').is(':checked'));
		localStorage.setItem("ng_tweet_copy", $('#ng_tweet_copy').is(':checked'));
		localStorage.setItem("ng_tweet_gomy", $('#ng_tweet_gomy').is(':checked'));
		localStorage.setItem("ng-dm-gelgit", $('#ng-dm-gelgit').is(':checked'));
		localStorage.setItem("nega_fav_rt", $('#nega_fav_rt').is(':checked'));
		localStorage.setItem("ng-es-pro", $('#nega-es-pro').is(':checked'));
		localStorage.setItem("nega-yum-pro", $('#nega-yum-pro').is(':checked'));
		localStorage.setItem("nega-hak-bos", $('#nega-hak-bos').is(':checked'));
		localStorage.setItem("nega-hak-az", $('#nega-hak-az').is(':checked'));
		localStorage.setItem("nega-giz-tak", $('#nega-giz-tak').is(':checked'));
		localStorage.setItem("ng-orj-kapak", $('#ng-orj-kapak').is(':checked'));
		localStorage.setItem("ng-spon-icerik", $('#ng-spon-icerik').is(':checked'));
		localStorage.setItem("ng-ht-tweet", $('#ng-ht-tweet').is(':checked'));
		localStorage.setItem("nega-ztn-tkp", $('#nega-ztn-tkp').is(':checked'));
		localStorage.setItem("min_tak_say", $('#min_tak_say').val());
		localStorage.setItem("max_tak_say", $('#max_tak_say').val());
		localStorage.setItem("kisi_bul_say", $('#kisi_bul_say').val());
		localStorage.setItem("ng-tkp-hiz", $('#ng-tkp-hiz').val());
		localStorage.setItem("ng-tkp-sys", $('#ng-tkp-sys').val());
		$(this).text("Kaydedildi");
	});
	$("#nega_tmn_sc").click(function(){
		if($(this).text() == "Tümünü seç"){
			$("#nega-sec-kayit").text("Kaydet");
			$("#nega-secenekler").find('input[type="checkbox"]').attr('checked', true);
			$(this).text("Tümünü kaldır")
		}else{
			$("#nega-sec-kayit").text("Kaydet");
			$("#nega-secenekler").find('input[type="checkbox"]').attr('checked', false);
			$(this).text("Tümünü seç")
		}
	})
})

$(document).ready(function() {
	if(localStorage.getItem("nega_rtlink") == "true"){
		$('#nega_rtlink').attr('checked', true);
	}
	else{
		$('#nega_rtlink').attr('checked', false);
	}

	if(localStorage.getItem("nega_turk_fav") == "true"){
		$('#nega_turk_fav').attr('checked', true);
	}
	else{
		$('#nega_turk_fav').attr('checked', false);
	}

	if(localStorage.getItem("nega_link_rt") == "true"){
		$('#nega_link_rt').attr('checked', true);
	}
	else{
		$('#nega_link_rt').attr('checked', false);
	}

	if(localStorage.getItem("ng_home_rtoff") == "true"){
		$('#ng_home_rtoff').attr('checked', true);
	}
	else{
		$('#ng_home_rtoff').attr('checked', false);
	}

	if(localStorage.getItem("ng_tweet_copy") == "true"){
		$('#ng_tweet_copy').attr('checked', true);
	}
	else{
		$('#ng_tweet_copy').attr('checked', false);
	}

	if(localStorage.getItem("ng_tweet_gomy") == "true"){
		$('#ng_tweet_gomy').attr('checked', true);
	}
	else{
		$('#ng_tweet_gomy').attr('checked', false);
	}

	if(localStorage.getItem("ng-dm-gelgit") == "true"){
		$('#ng-dm-gelgit').attr('checked', true);
	}
	else{
		$('#ng-dm-gelgit').attr('checked', false);
	}

	if(localStorage.getItem("nega_fav_rt") == "true"){
		$('#nega_fav_rt').attr('checked', true);
	}
	else{
		$('#nega_fav_rt').attr('checked', false);
	}

	if(localStorage.getItem("ng-orj-kapak") == "true"){
		$('#ng-orj-kapak').attr('checked', true);
	}
	else{
		$('#ng-orj-kapak').attr('checked', false);
	}

	if(localStorage.getItem("ng-spon-icerik") == "true"){
		$('#ng-spon-icerik').attr('checked', true);
	}
	else{
		$('#ng-spon-icerik').attr('checked', false);
	}

	if(localStorage.getItem("ng-ht-tweet") == "true"){
		$('#ng-ht-tweet').attr('checked', true);
	}
	else{
		$('#ng-ht-tweet').attr('checked', false);
	}

	if(localStorage.getItem("ng-es-pro") == "true"){
		$('#ng-es-pro').attr('checked', true);
	}
	else{
		$('#ng-es-pro').attr('checked', false);
	}

	if(localStorage.getItem("nega-yum-pro") == "true"){
		$('#nega-yum-pro').attr('checked', true);
	}
	else{
		$('#nega-yum-pro').attr('checked', false);
	}

	if(localStorage.getItem("nega-hak-bos") == "true"){
		$('#nega-hak-bos').attr('checked', true);
	}
	else{
		$('#nega-hak-bos').attr('checked', false);
	}

	if(localStorage.getItem("nega-hak-az") == "true"){
		$('#nega-hak-az').attr('checked', true);
	}
	else{
		$('#nega-hak-az').attr('checked', false);
	}

	if(localStorage.getItem("nega-giz-tak") == "true"){
		$('#nega-giz-tak').attr('checked', true);
	}
	else{
		$('#nega-giz-tak').attr('checked', false);
	}

	if(localStorage.getItem("nega-ztn-tkp") == "true"){
		$('#nega-ztn-tkp').attr('checked', true);
	}
	else{
		$('#nega-ztn-tkp').attr('checked', false);
	}
	if(localStorage.getItem("min_tak_say") == null){
		$('#min_tak_say').val("5000");
	}
	else{
		$('#min_tak_say').val(localStorage.getItem("min_tak_say"));
	}
	if(localStorage.getItem("max_tak_say") == null){
		$('#max_tak_say').val("15000");
	}
	else{
		$('#max_tak_say').val(localStorage.getItem("max_tak_say"));
	}
	if(localStorage.getItem("kisi_bul_say") == null){
		$('#kisi_bul_say').val("20");
	}
	else{
		$('#kisi_bul_say').val(localStorage.getItem("kisi_bul_say"));
	}
	if(localStorage.getItem("ng-tkp-sys") == null){
		$('#ng-tkp-sys').val("1000");
	}
	else{
		$('#ng-tkp-sys').val(localStorage.getItem("ng-tkp-sys"));
	}
	if(localStorage.getItem("ng-tkp-hiz") == null){
		$('#ng-tkp-hiz').val("600");
	}
	else{
		$('#ng-tkp-hiz').val(localStorage.getItem("ng-tkp-hiz"));
	}
})
$("h4.nega-sec-list > p > label, h4.nega-sec-list > p > input").click(function(){
	$("#nega-sec-kayit").text("Kaydet")
});


$(".paylasbuton").click(function(){
    var token = $("#signout-form > input.authenticity_token").attr('value');
    $.ajax({
        type: "POST",
        url: "  https://twitter.com/i/tweet/create",
        data: {
            authenticity_token: token,
            place_id: "",
            status: "Nega Twitter Araçları Eklentisini deneyin. http://www.nebigarci.net/?p=9129",
            tagged_users: ""
        },
        statusCode: {
            200: function() {
                $(".paylasbuton > a").text("Paylaşıldı")
            }
        }
    });
})
shortcut.add("Ctrl+Alt+T",function(event) {
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}
	else if($(".ProfileNav-item--following.is-active").length == 0 && $(".ProfileNav-item--followers.is-active").length == 0){
		alert("Bir kişinin takipçilerinde, takip ettiklerinde ya da kendi takipçilerinizde takip işlemi yapabilirsiniz.")
	}else{
		$("#liteyi_takip_et").click();
		    }
		},{
		    'type':'keydown',
		    'propagate':true,
		    'target':document
		});
	var ng_takip_sys = 1;
$("#liteyi_takip_et").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else if($(".ProfileNav-item--following.is-active").length == 0 && $(".ProfileNav-item--followers.is-active").length == 0){
		alert("Bir kişinin takipçilerinde, takip ettiklerinde ya da kendi takipçilerinizde takip işlemi yapabilirsiniz.")
	}else{
	    $("#liteyi_takip_et, #takipten_cik").addClass("visuallyhidden");
	    $("#takibi_durdur").removeClass("visuallyhidden");
	    $('#takibi_durdur').attr('id', 'takip_etmeyi_durdur');
	    takip_yap = setInterval(function(){
	        var kisi_sayisi = $('body').find('.Grid-cell.u-size1of2.u-lg-size1of3.u-mb10').length;
	        $(".ProfileClusterFollow").remove();
	        //yumurta profili takip etme
	        if(localStorage.getItem("nega-yum-pro") == "true"){
	        	$(".ProfileCard-avatarImage.js-action-profile-avatar").each(function(){
					var def_prof0 = "https://abs.twimg.com/sticky/default_profile_images/default_profile_0_bigger.png";
					var def_prof1 = "https://abs.twimg.com/sticky/default_profile_images/default_profile_1_bigger.png"
					var def_prof2 = "https://abs.twimg.com/sticky/default_profile_images/default_profile_2_bigger.png"
					var def_prof3 = "https://abs.twimg.com/sticky/default_profile_images/default_profile_3_bigger.png"
					var def_prof4 = "https://abs.twimg.com/sticky/default_profile_images/default_profile_4_bigger.png"
					var def_prof5 = "https://abs.twimg.com/sticky/default_profile_images/default_profile_5_bigger.png"
					var def_prof6 = "https://abs.twimg.com/sticky/default_profile_images/default_profile_6_bigger.png"
					var prf_img = $(this).attr("src");
					if(prf_img == def_prof0 || prf_img == def_prof1 || prf_img == def_prof2 || prf_img == def_prof3 || prf_img == def_prof4 || prf_img == def_prof5 || prf_img == def_prof6){
						$(this).parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove()
					}
				})
	        }
	        //hakkında boşsa takip etme//
	        if(localStorage.getItem("nega-hak-bos") == "true"){
	        	$(".ProfileCard-bio.u-dir:empty").parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove();
	        }
	        // gizli profilleri takip etme//
	        if(localStorage.getItem("nega-giz-tak") == "true"){
	        	$(".protected").parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove();
	        }
	        // profilinde az-09 yoksa takip etme
	        if(localStorage.getItem("nega-hak-az") == "true"){
				$(".ProfileCard-bio.u-dir, .ProfileNameTruncated-link.u-textInheritColor.js-nav.js-action-profile-name").each(function(){
					var txt = $(this).text();
					if(!txt.match(/[A-Za-z0-9]/) && txt.length !== 0){
						$(this).parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove()
						$(".ProfileCard-bio.u-dir[dir='rtl']").parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove()
					}
				});
			}
			//beni zaten takip ediyorsa takip etme //
	        if(localStorage.getItem("nega-ztn-tkp") == "true"){
	        	$(".FollowStatus").parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove();
	        }
			 //
	        $("div:not(.not-following) > .user-actions-follow-button, .UserActions-editButton.edit-button").parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove();
	        if(kisi_sayisi >= 18){
	            var usid = $(".GridTimeline").find(".js-stream-item:first-child").attr("data-item-id")
	            var token = $("#signout-form > input.authenticity_token").attr('value');
	            $.ajax({
	                type: "POST",
	                url: "https://twitter.com/i/user/follow",
	                data: {
		                authenticity_token: token,
		                challenges_passed:"false",
						handles_challenges:"1",
						impression_id:"",
						inject_tweet:"false",
						 user_id: usid
					},
	                statusCode: {
	                    400: function() {
	                        $('div.not-following:not(.protected) > button.js-follow-btn')[0].click();
	                        if ($('.alert-messages:not(.hidden)').css('top') === '46px') {
	                            clearInterval(takip_yap);
	                            clearInterval(kisi_yukle);
	                            $('#takip_etmeyi_durdur').attr('id', 'takibi_durdur');
	                            $("#takibi_durdur").addClass("visuallyhidden");
	                            $("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	                        }
	                    },
	                    200: function(){
	                   	 	$(".bird-topbar-etched").text(ng_takip_sys++);
	                	}
	                }
	            });
	            $(".GridTimeline").find(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10")[0].remove()
	        }
	        $(".message-text > a").each(function(){
	            if ($('.alert-messages:not(.hidden)').css('top') === '46px') {
	                $('#takip_etmeyi_durdur').attr('id', 'takibi_durdur');
	                $("#takibi_durdur").addClass("visuallyhidden");
	                $("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	                clearInterval(kisi_yukle);
	                clearInterval(takip_yap);
	            }
	        })
	        if(ng_takip_sys >= $('#ng-tkp-sys').val()){
	        	clearInterval(takip_yap);
		        clearInterval(kisi_yukle);
		        $('#takip_etmeyi_durdur').attr('id', 'takibi_durdur');
		        $("#takibi_durdur").addClass("visuallyhidden");
		        $("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	        }
	    }, $('#ng-tkp-hiz').val())

	    kisi_yukle = setInterval(function(){
	        var kisi_sayisi = $('body').find('.Grid-cell.u-size1of2.u-lg-size1of3.u-mb10').length;
	        if(kisi_sayisi <= 54){
	            $(window).scrollTop(0,document.body.scrollBottom);
	            setTimeout(function(){
	                window.scrollTo(0,document.body.scrollHeight);
	            },200);
	        }
	        if($(".GridTimeline").find(".GridTimeline-items").attr("data-min-position") == 0){
	            $(".user-actions.btn-group:not(.following) > .user-actions-follow-button.js-follow-btn").click();
	            $("#takip_etmeyi_durdur").click();
	            $(window).scrollTop(0,document.body.scrollBottom);
	            alert("Listenin sonuna geldiniz. Bu listede takip edecek kullanıcı kalmadı.")
	        }
	    },1600)
	    $("#takip_etmeyi_durdur").click(function(){
	        clearInterval(takip_yap);
	        clearInterval(kisi_yukle);
	        $('#takip_etmeyi_durdur').attr('id', 'takibi_durdur');
	        $("#takibi_durdur").addClass("visuallyhidden");
	        $("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	    });
	   	shortcut.add("Escape",function(e){
	        clearInterval(takip_yap);
	        clearInterval(kisi_yukle);
	        $('#takip_etmeyi_durdur').attr('id', 'takibi_durdur');
	        $("#takibi_durdur").addClass("visuallyhidden");
	        $("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	    },{
	        'type':'keydown',
	        'propagate':true,
	        'target':document
	    });
	}

});


//takipten çıkma kodları //
shortcut.add("Ctrl+Alt+U",function(event){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else if($(".ProfileNav-item--following.is-active").length == 0){
		alert("Sadece takip ettiklerinizin listesinde sizi geri takip etmeyenleri takipten çıkabilirsiniz.")
	}else{
    	$("#takipten_cik").click();
    }
},{
    'type':'keydown',
    'propagate':true,
    'target':document
});
	
$("#takipten_cik").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}
	else if($(".ProfileNav-item--following.is-active").length == 0){
		alert("Sadece takip ettiklerinizin listesinde sizi geri takip etmeyenleri takipten çıkabilirsiniz.")
	}else{
	    shortcut.add("Escape",function(e) {
	        $("#takibi_durdur").click();
	        $("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	    },{
	        'type':'keydown',
	        'propagate':true,
	        'target':document
	    });
	    $("#takibi_durdur").removeClass("visuallyhidden");
	    $("#liteyi_takip_et, #takipten_cik").addClass("visuallyhidden");
	    var ng_unf_sys = 1;
	    unf_basla = setInterval(function(){
	        var tk_edn = $(".FollowStatus").length;
	        var topl_ku = $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").length;
	        var tk_etm = topl_ku - tk_edn;
	        $(".FollowStatus, .not-following").parents(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").remove();
	        if(tk_etm >= 18){
	            var usid = $(".GridTimeline").find(".js-stream-item:first-child").attr("data-item-id")
	            var token = $("#signout-form > input.authenticity_token").attr('value');
	            $.ajax({
	                type: "POST",
	                url: "https://twitter.com/i/user/unfollow",
	                data: {authenticity_token: token, user_id: usid},
	                statusCode: {
	                    400: function() {
	                        alert("Beklenmedik bir sorun oluştu. Lütfen sayfayı yenileyip tekrar deneyin.");
	                        $("#takibi_durdur").click()
	                    },
	                    200: function(){

	                   		 $(".bird-topbar-etched").text(ng_unf_sys++);
	               		}
	                }
	            });
	            $(".GridTimeline").find(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10")[0].remove()
	        }
	    },100);
	    kisi_yukle_unf = setInterval(function(){
	        var tk_edn = $(".FollowStatus").length;
	        var topl_ku = $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").length;
	        var tk_etm = topl_ku - tk_edn;
	        if(tk_etm <= 54){
	            $(window).scrollTop(0,document.body.scrollBottom);
	            setTimeout(function(){
	                window.scrollTo(0,document.body.scrollHeight);
	            },200);
	        }
	        if($(".GridTimeline").find(".GridTimeline-items").attr("data-min-position") == 0){
	            $("div:not(.not-following) > .user-actions-follow-button").click();
	            clearInterval(unf_basla);
	        	clearInterval(kisi_yukle_unf);
	       		$("#takibi_durdur").addClass("visuallyhidden");
	       		$("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	            $(window).scrollTop(0,document.body.scrollBottom);
	        }
	    },1600)
	    $("#takibi_durdur").click(function(){
	        clearInterval(unf_basla);
	        clearInterval(kisi_yukle_unf);
	        $("#takibi_durdur").addClass("visuallyhidden");
	        $("#liteyi_takip_et, #takipten_cik").removeClass("visuallyhidden");
	    });
	}
});

///dm gönderme kodları //

$("#dmgonder").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else{
		$(window).scrollTop(0);
	    if(window.location.href == "https://twitter.com/followers"){
	        $(".Grid-cell.u-size2of3.u-lg-size3of4 > .Grid.Grid--withGutter").before("<form style='margin-top: 20px;' id='dm_gonderme_formu' class='hidden'><p>Kaç DM (direkt mesaj) gönderilsin? <input type='text' style='margin-left:10px' id='dm_gon_sayisi' value=''></input><input type='text' id='dm_bitirme' style='margin-left:10px' placeholder='ya da bu kullanıcı adına kadar gönder' title='Yazacağınız kullanıcı adına kadar mesaj gönderir ve durur.' value=''><input type='button' id='dmler_tamam' style='margin-left:10px' value='Gönder'></input></p><p style='text-align:center;margin: 10px 0px;font-size: 20px;'>Gönderilecek Mesajlar</p><p><input type='text' style='width:880px;margin:5px 0;' id='dm_0' value='Takip için teşekkür ederim.'></input></p><p><input type='text' style='width:880px;margin:5px 0;' id='dm_1' value='Beni Takip etmişsiniz. Teşekkürler.'></input></p> <p><input type='text' style='width:880px;margin:5px 0;'  id='dm_2' value='Takip listenize eklediğiniz için teşekkür ederim.'></input></p><p><input type='text' style='width:880px;margin:5px 0;' id='dm_3' value='Teşekkürler, takipte kalmanız dileğiyle.'></input></p><p><input type='text' style='width:880px;margin:5px 0;' id='dm_4' value='Teşekkürler takip için.'></input></p> <p><input type='text' style='width:880px;margin:5px 0;' id='dm_5' value='Takipten ötürü teşekkürler.';></input></p> <p><input type='text' style='width:880px;margin:5px 0;' id='dm_6' value='Takip için teşekkürler'></input></p><p><input type='text' style='width:880px;margin:5px 0;' id='dm_7' value='Takipte kalmanız dileğiyle sağolun.'></input></p><p><input type='text' style='width:880px;margin:5px 0;' id='dm_8' value='Teşekkürler iyi takipler.'></input></p><p><input type='text' style='width:880px;margin:5px 0;' id='dm_9' value='Takip için sağolun.'></input></p></form>");
	        $("#dm_gonderme_formu").removeClass("hidden");
	        if(!localStorage.getItem("dm_0") == ""){
	        	$('#dm_0').val(localStorage.getItem("dm_0"))
	        }
	        if(!localStorage.getItem("dm_1") == ""){
	        	$('#dm_1').val(localStorage.getItem("dm_1"))
	        }
	        if(!localStorage.getItem("dm_2") == ""){
	        	$('#dm_2').val(localStorage.getItem("dm_2"))
	        }
	        if(!localStorage.getItem("dm_3") == ""){
	        	$('#dm_3').val(localStorage.getItem("dm_3"))
	        }
	        if(!localStorage.getItem("dm_4") == ""){
	        	$('#dm_4').val(localStorage.getItem("dm_4"))
	        }
	        if(!localStorage.getItem("dm_5") == ""){
	        	$('#dm_5').val(localStorage.getItem("dm_5"))
	        }
	        if(!localStorage.getItem("dm_6") == ""){
	        	$('#dm_6').val(localStorage.getItem("dm_6"))
	        }
	        if(!localStorage.getItem("dm_7") == ""){
	        	$('#dm_7').val(localStorage.getItem("dm_7"))
	        }
	        if(!localStorage.getItem("dm_8") == ""){
	        	$('#dm_8').val(localStorage.getItem("dm_8"))
	        }
	        if(!localStorage.getItem("dm_9") == ""){
	        	$('#dm_9').val(localStorage.getItem("dm_9"))
	        }
	        $("#dmler_tamam").click(function(){
	        	localStorage.setItem("dm_0", $('#dm_0').val());
	        	localStorage.setItem("dm_1", $('#dm_1').val());
	        	localStorage.setItem("dm_2", $('#dm_2').val());
	        	localStorage.setItem("dm_3", $('#dm_3').val());
	        	localStorage.setItem("dm_4", $('#dm_4').val());
	        	localStorage.setItem("dm_5", $('#dm_5').val());
	        	localStorage.setItem("dm_6", $('#dm_6').val());
	        	localStorage.setItem("dm_7", $('#dm_7').val());
	        	localStorage.setItem("dm_8", $('#dm_8').val());
	        	localStorage.setItem("dm_9", $('#dm_9').val());
	            $("#dmgonder").addClass("dmgonderiliyor");
	            $("#dmgonder>a").text("Durdur");
	            shortcut.add("Escape",function(){
	                clearInterval(dmdm);
	                clearInterval(as);
	                $("#dmgonder>a").text("DM Gönder");
	                $("#dmgonder").removeClass("dmgonderiliyor");
	            },{
	                'type':'keydown',
	                'propagate':true,
	                'target':document
	            }); 
	            if($("#dm_bitirme").val() == '' && $("#dm_gon_sayisi").val() < 1){
	                alert("1'den daha küçük bir sayıda mesaj göndermeyiz!");
	                return false;
	            }
	            if($("#dm_0").val() == '' || $("#dm_1").val() == '' || $("#dm_2").val() == '' || $("#dm_3").val() == '' || $("#dm_4").val() == '' || $("#dm_5").val() == '' || $("#dm_6").val() == '' || $("#dm_7").val() == '' || $("#dm_8").val() == '' || $("#dm_9").val() == ''){
	                alert("Lütfen boş mesaj bırakmayın.");
	                return false;
	            }
	            $("#dm_gonderme_formu").addClass("hidden");
	            var dmbs = 0;
	            if($("#dm_gon_sayisi").val() === ''){
	                var dmlimit = 250;
	            }
	            else{
	                var dmlimit = $("#dm_gon_sayisi").val();
	            }
	            var dmdm = setInterval(function(){
	                if(dmbs++ >= dmlimit){
	                    clearInterval(dmdm);
	                    clearInterval(as);
	                    window.alert(dmlimit+' kişiye mesaj başarıyla gönderildi.')
	                    $("#dmgonder>a").text("DM Gönder");
	                    $("#dmgonder").removeClass("dmgonderiliyor");
	                    return false;   
	                }
	                var ka = $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").find(".ProfileCard.js-actionable-user").attr('data-screen-name');
	                if($("#dm_bitirme").val() == ka){
	                    clearInterval(dmdm);
	                    clearInterval(as);
	                    window.alert(ka+' kullanıcı adlı kişiye kadar mesaj gönderildi.')
	                    $("#dmgonder>a").text("DM Gönder");
	                    $("#dmgonder").removeClass("dmgonderiliyor");
	                    return false;
	                }
	                $(".user-dropdown.dropdown-toggle")[0].click();
	                $(".mention-text.pretty-link.not-blocked> button")[0].click();
	                var dmler = new Array()
	                dmler[0] = $("#dm_0").val();
	                dmler[1] = $("#dm_1").val();
	                dmler[2] = $("#dm_2").val();
	                dmler[3] = $("#dm_3").val();
	                dmler[4] = $("#dm_4").val();
	                dmler[5] = $("#dm_5").val();
	                dmler[6] = $("#dm_6").val();
	                dmler[7] = $("#dm_7").val();
	                dmler[8] = $("#dm_8").val();
	                dmler[9] = $("#dm_9").val();
	                var i = Math.floor(10*Math.random());
	                var kism = $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10").find(".ProfileCard.js-actionable-user").attr('data-screen-name');
	                document.getElementById("tweet-box-global").innerHTML = "m "+kism+" "+dmler[i]+"";
	                setTimeout(function(){
	                    $(".btn.primary-btn.tweet-action.tweet-btn.js-tweet-btn.messaging").click();
	                },2000);
	                $(".Grid-cell.u-size1of2.u-lg-size1of3.u-mb10")[0].remove();
	                $(".dmgonderiliyor").click(function(){
	                    $("#dmgonder>a").text("DM Gönder");
	                    clearInterval(dmdm);
	                    clearInterval(as);
	                    $("#dmgonder").removeClass("dmgonderiliyor");
	                });
	            },5000)
	            var as = setInterval(function() {
	                var kisi_sayisi = $('body').find('.Grid-cell.u-size1of2.u-lg-size1of3.u-mb10').length;
	                if(kisi_sayisi < 18){
	                    window.scrollTo(0,document.body.scrollHeight);
	                    setTimeout(function() {
	                        $(window).scrollTop(0,document.body.scrollBottom);
	                    },1000);
	                }
	            },10000);
	        });
	    }
	    else{
	        alert("Bu sayfada DM gönderemezsiniz. Lütfen takipçiler sayfasına gidin.")
	    }
	}
});

//dm silme kodları //

$(".DMActivity.DMInbox.js-ariaDocument.DMActivity--open").find(".DMActivity-toolbar").before('<a style="cursor:pointer;color:red;margin-right:10px" id="ng_dm_sil">Temizle</a>');
$("a#ng_dm_sil").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else{
	    if(confirm("Bu listedeki tüm mesajlar silinecek!") == true) {
	        dm_siliniyor = setInterval(function(){
	            var dm_sys = $(".DMInbox-conversationItem").length;
	            $(".u-scrollY").scrollTop($(".DMInbox-conversations").height())
	            setTimeout(function(){
	                $(".u-scrollY").scrollTop(0)
	            },200)
	            if(dm_sys == 0){
	                clearInterval(dm_siliniyor);
	            }else{
	                var token = $("#signout-form > input.authenticity_token").attr("value");
	                var dmid = $(".DMInbox-conversationItem:not(.hidden) > .DMInboxItem:first-child").attr("data-thread-id")
	                var lastts = localStorage.getItem("__DM__:latestNotificationTimestamp");
	                $.ajax({
	                    type: "POST",
	                    url: "https://twitter.com/messages/with/conversation",
	                    data: {
	                        _method: "DELETE",
	                        authenticity_token: token,
	                        cursor: "",
	                        end_conversation:"false",
	                        id: dmid,
	                        last_note_ts: lastts,
	                    },
	                    statusCode: {
	                        200: function() {
	                            $(".DMInbox-conversationItem:not(.hidden):first-child").remove()
	                        },
	                        500: function(){
	                          clearInterval(dm_siliniyor);  
	                        }
	                    }
	                });
	            }
	        },300)
	    }
	}
})

///fav yapma kodları //

$("#favyap").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else{
		if($("#favyap").text() == "Durdur"){
	        clearInterval(favla);
	        $("#favyap").text("Fav Yap")
	    }
	    else{
		    if($(".route-home").length == "1") {
		        $("#favyap").text("Durdur")
		        favla = setInterval(function(){
		        	if(localStorage.getItem("nega_fav_rt") == "true"){
		        		$(".Icon.Icon--small.Icon--retweeted").parents(".js-stream-item.stream-item.stream-item").remove()
		        	}
		        	if(localStorage.getItem("nega_link_rt") == "true"){
			        	$("p.js-tweet-text.tweet-text").each(function(){
							if(! $(this).find("a:not(.twitter-hashtag)").length == 0){
						    	$(this).parents(".js-stream-item.stream-item.stream-item").remove()
							}
						})
					}
		        	if(localStorage.getItem("nega_turk_fav") == "true"){
						$(".TweetTextSize.js-tweet-text.tweet-text").each(function(){
						var dili = $(this).attr("lang")
							if(dili != "tr"){
								$(this).parents(".js-stream-item.stream-item.stream-item").remove()
							}
						})
					}	
		            $(".favorited").parents(".js-stream-item.stream-item.stream-item.expanding-stream-item").remove();
		            var yeni_tweet = $(".stream-container").find(".new-tweets-bar.js-new-tweets-bar").attr('data-item-count');
		            var tweet = $('.stream-items.js-navigable-stream >.js-stream-item.stream-item.stream-item.expanding-stream-item').length;
		            if(tweet > 0){
		                $(".ProfileTweet-actionButton.js-actionFavorite")[0].click()
		                setTimeout(function(){
		                    $('.js-stream-item.stream-item.stream-item.expanding-stream-item')[0].remove();
		                },250);
		            }
		            if(tweet < 2 || yeni_tweet > 0){
		                $("#global-nav-home > a").click()
		                $(".new-tweets-bar.js-new-tweets-bar").click();
		            }
		            if ($('.alert-messages:not(.hidden)').css('top') === '46px') {
					    $("#favyap").text("Fav Yap");
	        			clearInterval(favla);
	                }
		        },500);
		    }
			else if($(".route-profile").length == "1" && $(".ProfileNav-item.ProfileNav-item--tweets.is-active").length == "1"){
		        $("#favyap").text("Durdur")
		        favla = setInterval(function(){
		        	if(localStorage.getItem("nega_fav_rt") == "true"){
		        		$(".Icon.Icon--small.Icon--retweeted").parents(".js-stream-item.stream-item.stream-item").remove()
		        	}
		        	if(localStorage.getItem("nega_link_rt") == "true"){
			        	$(".ProfileTweet-text.js-tweet-text").each(function(){
							if(! $(this).find("a:not(.twitter-hashtag)").length == 0){
						    	$(this).parents(".Grid[data-component-term='tweet']").remove();
							}
						})
					}
		            $(".favorited").parents(".js-stream-item.stream-item.stream-item.expanding-stream-item").remove();
		            var tweet = $('.stream-items.js-navigable-stream >.js-stream-item.stream-item.stream-item.expanding-stream-item').length;
		            var sontweet = $("#timeline > .stream-container").attr("data-min-position");
		            var sontweetyok = $("#timeline > .stream-container[data-min-position]").length;
		            if(tweet > 0){
		                $(".ProfileTweet-actionButton.js-actionFavorite")[0].click()
		                setTimeout(function(){
		                    $('.stream-items.js-navigable-stream >.js-stream-item.stream-item.stream-item.expanding-stream-item')[0].remove();
		                },250);
		            }
		            if(tweet < 3 ){
		                window.scrollTo(0,document.body.scrollHeight);
		                setTimeout(function() {
		                    $(window).scrollTop(0,document.body.scrollBottom);
		                },1000);
		            }
		            if(sontweet == 0 || sontweetyok == 0){
		            	$(".favorited").parents(".js-stream-item.stream-item.stream-item.expanding-stream-item").remove();
		            	$(".ProfileTweet-actionButton.js-actionButton.js-actionFavorite.js-tooltip").click()
		            	clearInterval(favla);
		       			$("#favyap").text("Fav Yap");
		            }
		            if($('.alert-messages:not(.hidden)').css('top') === '46px') {
					    $("#favyap").text("Fav Yap");
	        			clearInterval(favla);
	                }
		        },500);
			}else if($(".AppContent.wrapper-search").length == "1"){
		        $("#favyap").text("Durdur")
		        favla = setInterval(function(){
		        	if(localStorage.getItem("nega_fav_rt") == "true"){
		        		$(".Icon.Icon--small.Icon--retweeted").parents(".js-stream-item.stream-item.stream-item").remove()
		        	}
		        	if(localStorage.getItem("nega_link_rt") == "true"){
			        	$(".js-tweet-text.tweet-text").each(function(){
							if(! $(this).find("a:not(.twitter-hashtag)").length == 0){
						    	$(this).parents(".js-stream-item.stream-item.stream-item").remove();
							}
						})
					}
					if(localStorage.getItem("nega_turk_fav") == "true"){
						$(".TweetTextSize.js-tweet-text.tweet-text").each(function(){
						var dili = $(this).attr("lang")
							if(dili != "tr"){
								$(this).parents(".js-stream-item.stream-item.stream-item").remove()
							}
						})
					}	
		            $(".favorited").parents(".js-stream-item.stream-item.stream-item.expanding-stream-item").remove();
		            var tweet = $('.stream-items.js-navigable-stream >.js-stream-item.stream-item.stream-item.expanding-stream-item').length;
		            var sontweet = $("#timeline > .stream-container").attr("data-min-position");
		            var sontweetyok = $("#timeline > .stream-container[data-min-position]").length;
		            if(tweet > 0){
		                $(".ProfileTweet-actionButton.js-actionFavorite")[0].click()
		                setTimeout(function(){
		                    $('.stream-items.js-navigable-stream >.js-stream-item.stream-item.stream-item.expanding-stream-item')[0].remove();
		                },250);
		            }
		            if(tweet < 2 || sontweet > 0){
		                $(".new-tweets-bar.js-new-tweets-bar").each(function(){
		                	$(this).click();
		                })
		            }
		            if ($('.alert-messages:not(.hidden)').css('top') === '46px') {
					    $("#favyap").text("Fav Yap");
	        			clearInterval(favla);
	                }
		            if(sontweet == 0 || sontweetyok == 0){
		            	$(".favorited").parents(".js-stream-item.stream-item.stream-item.expanding-stream-item").remove();
		            	$(".ProfileTweet-actionButton.js-actionButton.js-actionFavorite.js-tooltip").click()
		            	clearInterval(favla);
		       			$("#favyap").text("Fav Yap");
		            }
		            if($('.alert-messages:not(.hidden)').css('top') === '46px') {
					    $("#favyap").text("Fav Yap");
	        			clearInterval(favla);
	                }
		        },500);
			}else{
				alert("Bu sayfada favoriye ekleme yapılamaz. Lütfen Anasayfa'ya, hashtag'e, arama sonuçlarına ya da bir kişinin profiline (tweetlerine) gidin.")
			}
	    }
	    shortcut.add("Escape",function(){
	        $("#favyap").text("Fav Yap");
	        clearInterval(favla);
	    },{
	        'type':'keydown',
	        'propagate':true,
	        'target':document
	    });
	}
})


// favori silme //
$("#favsil").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else{
		if($("#favsil").text() == "Durdur"){
			clearInterval(unfavori);
			clearInterval(favkontrol);
			$("#favsil").text("Fav Sil")
		}
		else if($(".route-profile").length == "1" && $(".ProfileNav-item.ProfileNav-item--favorites.is-active").length == "1"){
			$("#favsil").text("Durdur");
			unfavori = setInterval(function(){
				$('.stream-items > .js-stream-item.stream-item.stream-item').each(function(){
					$('.stream-items > .js-stream-item.stream-item.stream-item').find(".ProfileTweet-actionButton.js-actionFavorite")[0].click();
					$('.stream-items > .js-stream-item.stream-item.stream-item')[0].remove();
				})
				if($(".stream-container[data-min-position]").length == 0){
					clearInterval(unfavori);
				}
			},500)
			favkontrol = setInterval(function(){
				var tweetsys = $('.stream-items > .js-stream-item.stream-item.stream-item').length;
				if(tweetsys < 50 || tweetsys == 50){
					$(window).scrollTop(0,document.body.scrollBottom);
					setTimeout(function(){
						window.scrollTo(0,document.body.scrollHeight);
					},200);
				}
					if($(".stream-container[data-min-position]").length == 0){
					clearInterval(favkontrol)
				}
			},3000)
		}else{
			alert("Bu sayfada favori silme işlemi yapılamaz. Lütfen favorilerinizin olduğu sayfaya gidin.")
		}
	}
	shortcut.add("Escape",function(){
		$("#favsil").text("Fav Sil");
		clearInterval(unfavori);
		clearInterval(favkontrol);
	},{
		'type':'keydown',
		'propagate':true,
		'target':document
	});
})

// rt yapma kodu // 
$("#rtyap").click(function(){
	var nega_ctrl = $("#ng_hsp_ctrl").length;
	var nega_stnl_msg = "E"+"k"+"l"+"e"+"n"+"t"+"i"+"y"+"i"+" "+"y"+"e"+"t"+"k"+"i"+"s"+"i"+"z"+" "+"ş"+"e"+"k"+"i"+"l"+"d"+"e"+" "+"k"+"u"+"l"+"l"+"a"+"n"+"m"+"a"+"y"+"a"+" "+"ç"+"a"+"l"+"ı"+"ş"+"t"+"ı"+"n"+"ı"+"z";
	if(nega_ctrl > 0){
		alert(nega_stnl_msg)
	}else{
		if($("#rtyap").text() == "Durdur"){
	        clearInterval(rtle);
	        $("#rtyap").text("RT Yap")
	    }
	    else{
		    if($(".route-home").length == "1") {
		        $("#rtyap").text("Durdur")
		        rtle = setInterval(function(){
		        	$(".Icon.Icon--small.Icon--retweeted").parents(".js-stream-item.stream-item.stream-item").remove()
		        	$(".Icon--promotedGray").parents(".js-stream-item").remove()
		        	if(localStorage.getItem("nega_rtlink") == "true"){
				        $("p.js-tweet-text.tweet-text").each(function(){
							if(! $(this).find("a:not(.twitter-hashtag)").length == 0){
							    	$(this).parents(".js-stream-item.stream-item.stream-item").remove()
							}
						})
					}	
		            $(".tweet.retweeted").parents(".js-stream-item").remove()
		            var new_tweet = $(".stream-container").find(".new-tweets-bar.js-new-tweets-bar").attr('data-item-count');
		            var rttweet = $('.stream-items.js-navigable-stream >.js-stream-item.stream-item.stream-item.expanding-stream-item').length;
		            if(rttweet > 0){
		            	$(".Icon--promotedGray").parents(".js-stream-item").remove()
		            	$(".js-actionRetweet")[0].click()
		                $(".retweet-action").click()
		                setTimeout(function(){
		                    $(".js-stream-item.stream-item.stream-item")[0].remove();
		                },250);
		            }
		            if(rttweet < 2 || new_tweet > 0){
		                $("#global-nav-home > a").click()
		                $(".new-tweets-bar.js-new-tweets-bar").click();
		            }
		            if ($('.alert-messages:not(.hidden)').css('top') === '46px') {
					    $("#rtyap").text("RT Yap");
	        			clearInterval(rtle);
	                }
		        },500);
		    }
			else if($(".route-profile").length == "1" && $(".ProfileNav-item.ProfileNav-item--tweets.is-active").length == "1"){
		        $("#rtyap").text("Durdur")
		        rtle = setInterval(function(){
		        	$(".tweet.retweeted").parents(".js-stream-item").remove()
		        	$(".Icon.Icon--small.Icon--retweeted").parents(".js-stream-item.stream-item.stream-item").remove()
		            var rttweet = $('.stream-items.js-navigable-stream >.js-stream-item.stream-item.stream-item.expanding-stream-item').length;
		            var rtsontweet = $("#timeline > .stream-container").attr("data-min-position");
		            var rtsontweetyok = $("#timeline > .stream-container[data-min-position]").length;
		            if(rttweet > 0){
		                $(".js-actionRetweet")[0].click()
		                $(".retweet-action").click()
		                setTimeout(function(){
		                    $(".tweet.retweeted").parents(".js-stream-item").remove()
		                },250);
		            }
		            if(rttweet < 3 ){
		                window.scrollTo(0,document.body.scrollHeight);
		                setTimeout(function() {
		                    $(window).scrollTop(0,document.body.scrollBottom);
		                },1000);
		            }
		            if(rtsontweet == 0 || rtsontweetyok == 0){
		            	$(".retweeted").parents(".js-stream-item.stream-item.stream-item.expanding-stream-item").remove();
		            	clearInterval(rtle);
		       			$("#rtyap").text("RT Yap");
		            }
		            if($('.alert-messages:not(.hidden)').css('top') === '46px') {
					    $("#rtyap").text("RT Yap");
	        			clearInterval(rtle);
	                }
		        },500);
			}else{
				alert("Bu sayfada favoriye ekleme yapılamaz. Lütfen Anasayfa'ya ya da bir kişinin profiline (tweetlerine) gidin.")
			}
	    }
	    shortcut.add("Escape",function(){
	        $("#rtyap").text("RT Yap");
	        clearInterval(favla);
	    },{
	        'type':'keydown',
	        'propagate':true,
	        'target':document
	    });
	}
})


// profil bağlantısı //

if(localStorage.getItem("ng-es-pro") == "true"){
	$("body.logged-in").each(function(){
		$("#nega-es-pro").prop('checked', true);
		var kullanici_adim = $(".account-group.js-mini-current-user").attr("data-screen-name");
		$(".nav.js-global-actions > li").last().after('<li id="ben_link" class="profile"><a role="button" href="/'+kullanici_adim+'" class="js-tooltip js-dynamic-tooltip" data-placement="bottom" data-original-title=""><span class="Icon Icon-porfile Icon--large"></span><span class="text">Profil</span><span class="count-inner"></span></a></li>');
		$('head').append('<style>.Icon-porfile::before{ content:"\\f056" }</style>');
	})
}

$(window).scroll(function(){
	///hashtag Tweetleyici ///
	if(localStorage.getItem("ng-ht-tweet") == "true" && $(".ht_tweet").length < 1){
		$(".trend-item.js-trend-item > a").after(" <img class='ht_tweet' title='Tweetle' src='https://abs.twimg.com/emoji/v1/72x72/1f4e3.png' width='15' height='15'>")
		$(".ht_tweet").click(function(){
			var h_tag = $(this).parents(".trend-item.js-trend-item").attr("data-trend-name");
			$("#global-new-tweet-button").click();
			$("#tweet-box-global").html(h_tag + " ")
		})			
	}
	//sponsorlu içerik kaldırıcı//
	if(localStorage.getItem("ng-spon-icerik") == "true" && $(".dismiss-promoted").length > 0){
		$(".dismiss-promoted").parents(".js-stream-item.stream-item").remove()
	}
	if(localStorage.getItem("ng-spon-icerik") == "true" ){
		$(window).scroll(function(){
			$(".promoted-trend").remove()
		})
	}
	//kapak fotoğrafını göster//
	if(localStorage.getItem("ng-orj-kapak") == "true" && $(".route-profile").length == 1){
		if($("#nega_kapak_fo").length == 0){
				var prof_header = $(".ProfileCanopy-headerBg > img").attr("src").replace("/1500x500","")
		$(".ProfileCanopy-header.u-bgUserColor").before('<a id="nega_kapak_fo" href='+prof_header+' data-resolved-url-large='+prof_header+' target="_blank" style="  position: absolute;float: right;right: 17px;top: 270px;z-index: 999999999999;background: rgba(0, 0, 0, 0.48);height: 25px;line-height: 25px;padding: 6px;color: #ddd;text-decoration: none;">Kapak fotoğrafını göster</a>');
		}
	}
})
