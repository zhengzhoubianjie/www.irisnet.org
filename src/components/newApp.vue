<template>
    <div class="mobile_container">
        <div class="app">
            <div class="head">
                <img src="../assets/app/irislogo.png" class="imglogo" @click="toHome">
                <div class="div_en">
                    <a href="?lang=CN" v-if="$store.state.lang!='CN'">
                        CN
                    </a>
                    <a href="?lang=EN" v-if="$store.state.lang=='CN'">
                        EN
                    </a>
                    <img src="../assets/app/list.png" @click="menuIs=!menuIs"/>
                </div>
            </div>
            <div class="menu" v-show="menuIs">
                <section>
                    <a @click="skipMainnet">{{$store.state.lang=='CN'? '主网' :'Mainnet'}}</a>
                </section>
                <section>
                    <a @click="skipTestNet">{{$store.state.lang=='CN'?'测试网':'Testnet'}}</a>
                </section>
                <section v-for="(item,index) in links">
                    <a v-if="item.href.indexOf('ttp')==-1" :href="item.href" @click="closeMenu()">
                        {{item.txt}}
                    </a>
                    <a v-if="item.href.indexOf('ttp')!=-1" :href="'h'+item.href" @click="closeMenu()">
                        {{item.txt}}
                    </a>
                </section>
                <section>
                    <a :href="$store.state.lang=='CN' ? 'https://www.irisnet.org/docs/zh/' : 'https://www.irisnet.org/docs/'" target="_blank">{{$store.state.lang=='CN'?'文档':'Docs'}}</a>
                </section>
                <section>
                    <a class="item medium_img_content" :href="$store.state.lang=='CN' ? 'https://medium.com/irisnet-blog' : 'https://medium.com/irisnet-blog' " target="_blank">
                        <span>{{$store.state.lang=='CN'?'博客':'Blog'}}</span>
                        <img class="medium_img" src="../assets/mobile_medium.png">
                    </a>
                </section>
            </div>

            <div id="#/0" class="swipe_content" style="height: 100%;">
                <swipe ref="swipe" class="my-swipe" @change="imgChange" :auto="10000" v-if="active">
                    <swipe-item v-for="(item,index) in $store.state.messages.mobileLogo" :key="index">
                        <a :href="index== 1 ? $store.state.lang=='CN' ? 'https://mp.weixin.qq.com/s/nN6I8raVV9uq-lsmfi8mvg' : 'https://medium.com/irisnet-blog/opened-irisnet-bug-bounty-program-for-mainnet-launch-30627e00e2e' : 'javascript:;' "
                           target="_blank" @click="handleSwipeLink(index)">
                            <img class="index1_logo" :src="item.src"/>
                        </a>
                    </swipe-item>
                </swipe>
            </div>
            <div class="container">
                <div style="width: 100%;height: auto">
                    <div id="#/0/1" class="about">
                        <div class="about_warp">
                            <div class="about_txt">
                                <div class="title-txt">
                                    {{$store.state.messages.about.title}}
                                    <div class="nav-line"></div>
                                </div>
                                <div class="about_div">
                                    {{$store.state.messages.about.txt[0]}}
                                </div>
                                <div class="about_div">
                                    {{$store.state.messages.about.txt[1]}}
                                </div>
                                <div class="about_div">
                                    {{$store.state.messages.about.txt[2]}}
                                </div>
                                <div class="whiteBook-button">
                                    <a class="whiteHref-btn" :href="$store.state.messages.whiteHref">{{$store.state.messages.about.btnTxt}}</a>
                                    <i class="guide_right">
                                        <img src="../../public/arrowhead.png">
                                    </i>
                                </div>
                                <div class="img_right_container">
                                    <div class="img_containter_top">
                                        <div class="img_default_containter">
                                            <img src="../../public/iris.png">
                                        </div>
                                        <div class="rectangle_default_container">
                                            <img src="../../public/Rectangle_one.png">
                                        </div>
                                    </div>

                                    <div class="img_container_bottom">
                                        <div>
                                            <div class="img_default_containter">
                                                <img src="../../public/chain.png">
                                            </div>
                                            <div class="rectangle_default_container">
                                                <img src="../../public/Rectangle_two.png">
                                            </div>
                                        </div>
                                        <div class="img-center-container">
                                            <div class="img_default_containter">
                                                <img src="../../public/cosmos.png">
                                            </div>
                                            <div class="rectangle_default_container">
                                                <img src="../../public/Rectangle_three.png">
                                            </div>
                                        </div>
                                        <div>
                                            <div class="img_default_containter">
                                                <img src="../../public/Rectangle-five.png">
                                            </div>
                                            <div class="rectangle_default_container">
                                                <img src="../../public/Rectangle_four.png">
                                            </div>
                                        </div>
                                    </div>
                                </div>

                            </div>
                        </div>
                    </div>
                    <div id="#/0/2" class="network">
                        <div class="network_title">
                            <div class="what_txt_title" style="font-size: 30px;margin-bottom: 10px;color:#fff">
                                {{$store.state.messages.network.title}}
                                <div class="nav-line"></div>
                            </div>
                            <div class="what_txt_list_two">
                                {{$store.state.messages.network.txt[0]}}
                            </div>
                            <div class="what_txt_list_center">
                                {{$store.state.messages.network.txt[1]}}
                            </div>
                            <div class="what_txt_list_four">
                                {{$store.state.messages.network.txt[2]}}
                            </div>
                            <img src="../assets/app/diagram.png"/>
                        </div>
                    </div>

                    <div id="#/0/4" class="roadmap">
                        <div class="roadmap_title">
                            {{$store.state.messages.roadmap.title}}
                            <div class="nav-line"></div>
                        </div>
                        <div class="roadmap_warp">
                            <div style="width: 2px;height: 120%;background: #724be3" class="rainbow"></div>
                            <div class="roadmap_div" style="top:0;">
                                <div class="roadmap_radius" @click="txtShow(0)">
                                    <div class="direction-line" :class="list[0].is ? 'showAnim' : 'show-line'"></div>
                                    <img src="../../public/app/Ellipse2.png">
                                    <div class="show-radius" :class="list[0].is ? 'show-scale' : ''"></div>
                                </div>
                                <div v-if="$store.state.lang=='CN'" class="roadmap_img" @click="txtShow(0)">
                                    <span>盘古</span>
                                    <p>2018年1月 </p>
                                    <p> | </p>
                                    <p>2019年3月</p>
                                </div>
                                <div v-if="$store.state.lang!='CN'" class="roadmap_img" @click="txtShow(0)">
                                    <span>PANGU</span>
                                    <p>JAN 2018 </p>
                                    <p> | </p>
                                    <p>MAR 2019</p>
                                </div>
                                <div class="roadmap_txt" :class=" list[0].is ? 'showOpacity' : '' ">
                                    {{$store.state.messages.roadmap.list[0].txt}}
                                </div>
                            </div>
                            <div class="roadmap_div" style="top:33%;">
                                <div class="roadmap_radius" @click="txtShow(1)">
                                    <div class="direction-line" :class="list[1].is ? 'showAnim' : 'show-line'"></div>
                                    <img src="../../public/app/Ellipse2.png">
                                    <div class="show-radius" :class="list[1].is ? 'show-scale' : ''"></div>
                                </div>
                                <div v-if="$store.state.lang=='CN'" class="roadmap_img" @click="txtShow(1)">
                                    <span>女娲</span>
                                    <p>2019年4月 </p>
                                    <p> | </p>
                                    <p>2019年9月</p>
                                </div>
                                <div v-if="$store.state.lang!='CN'" class="roadmap_img" @click="txtShow(1)">
                                    <span>NÜWA</span>
                                    <p>APR 2019 </p>
                                    <p> | </p>
                                    <p>SEPT 2019</p>
                                </div>
                                <div class="roadmap_txt" :class=" list[1].is ? 'showOpacity' : '' ">
                                    {{$store.state.messages.roadmap.list[1].txt}}
                                </div>
                            </div>
                            <div class="roadmap_div" style="top:66%;">
                                <div class="roadmap_radius" @click="txtShow(2)">
                                    <div class="direction-line" :class="list[2].is ? 'showAnim' : 'show-line'"></div>
                                    <img src="../../public/app/Ellipse2.png">
                                    <div class="show-radius" :class="list[2].is ? 'show-scale' : ''"></div>
                                </div>
                                <div v-if="$store.state.lang=='CN'" class="roadmap_img" @click="txtShow(2)">
                                    <span>夸父</span>
                                    <p>2019年10月</p>
                                    <p> | </p>
                                    <p>2019年12月</p>
                                </div>
                                <div v-if="$store.state.lang!='CN'" class="roadmap_img" @click="txtShow(2)">
                                    <span>KUAFU</span>
                                    <p>OCT 2019 </p>
                                    <p> | </p>
                                    <p>DEC 2019</p>
                                </div>
                                <div v-if="$store.state.lang!='CN'" class="roadmap_txt"
                                     :class=" list[2].is ? 'showOpacity' : '' " style="top: -54px;">
                                    {{$store.state.messages.roadmap.list[2].txt}}
                                </div>
                                <div v-if="$store.state.lang=='CN'" class="roadmap_txt"
                                     :class=" list[2].is ? 'showOpacity' : '' " style="top: 0;">
                                    {{$store.state.messages.roadmap.list[2].txt}}
                                </div>
                            </div>
                            <div class="roadmap_div" style="top:99%;">
                                <div class="roadmap_radius" @click="txtShow(3)">
                                    <div class="direction-line" :class="list[3].is ? 'showAnim' : 'show-line'"></div>
                                    <img src="../../public/app/Ellipse2.png">
                                    <div class="show-radius" :class="list[3].is ? 'show-scale' : ''"></div>
                                </div>
                                <div v-if="$store.state.lang=='CN'" class="roadmap_img" @click="txtShow(3)">
                                    <span>后羿</span>
                                    <p>2020年1月 </p>
                                    <p>之后</p>
                                </div>
                                <div v-if="$store.state.lang!='CN'" class="roadmap_img" @click="txtShow(3)">
                                    <span>HOUYI</span>
                                    <p>BEYOND </p>
                                    <p>JAN 2020</p>
                                </div>
                                <div v-if="$store.state.lang!='CN'" class="roadmap_txt"
                                     :class=" list[3].is ? 'showOpacity' : '' " style="top: -70px;">
                                    {{$store.state.messages.roadmap.list[3].txt}}
                                </div>
                                <div v-if="$store.state.lang=='CN'" class="roadmap_txt"
                                     :class=" list[3].is ? 'showOpacity' : '' " style="top: 0;">
                                    {{$store.state.messages.roadmap.list[3].txt}}
                                </div>
                            </div>
                        </div>
                    </div>

                    <div id="#/0/3" class="collaboration">
                        <div class="collaboration_wrap">
                            <h2>{{collaboration_title}}</h2>
                            <div class="nav-line"></div>

                            <div class="collaboration_one_col">
                                <article class="investment">
                                    <h4>{{collaboration_core.title}}</h4>
                                    <comp-collaboration-item :info="collaboration_core"></comp-collaboration-item>
                                </article>
                            </div>

                            <div class="collaboration_one_col">
                                <article class="investment">
                                    <h4>{{collaboration_strategy.title}}</h4>
                                    <comp-collaboration-item :info="collaboration_strategy"></comp-collaboration-item>
                                </article>
                            </div>
                            <div class="collaboration_two_col">
                                <article class="strategy">
                                    <h4>{{collaboration_ecosystem.title}}</h4>
                                    <comp-collaboration-item :info="collaboration_ecosystem"></comp-collaboration-item>
                                </article>
                            </div>
                            <div class="collaboration_one_col">
                                <article class="investment">
                                    <h4>{{collaboration_investment.title}}</h4>
                                    <span class="subtitle-text">{{collaboration_investment.subtitle}}</span>
                                    <comp-collaboration-item :info="collaboration_investment"></comp-collaboration-item>
                                </article>
                            </div>
                        </div>
                    </div>
                    <div id="#/0/5" class="what model_upcoming_content_wrap">
                    </div>
                    <div id="#/0/6" class="contact" style="background: #0f0f1f;">
                        <div class="contact_title">
                            {{$store.state.messages.contact.title}}
                            <div class="nav-line"></div>
                        </div>
                        <div class="app-mail-container">
                            <div class="app-getmail-container">
                                <span>{{$store.state.messages.newsLetter.letter}}</span>
                            </div>
                            <div class="app-ipt-container">
                                <input :class="showerr ? 'erript' : ''" v-model="mailaddress" type="text" :placeholder=$store.state.messages.placehooder.placehooder>
                                <p :class="showerr ? '' : 'app-showerrcontainer'" class="errcontainer">{{$store.state.messages.errEmail.err}}</p>
                            </div>
                            <div class="app-sub-container" @click="commitMaile">
                                <span>{{subscription}}</span>
                            </div>
                        </div>
                        <div class="contact_div">
                            <div class="img-container">
                                <a :href="item.href" target="_blank" style="overflow: hidden"
                                   @click="blank(item.txt)"
                                   v-for="item in $store.state.messages.appcontact.appimg">
                                    <div class="contact_radius">
                                        <img :src="UrlSrc+item.src"/>
                                    </div>
                                </a>
                            </div>
                            <div class="img-container">
                                <a :href="item.href" target="_blank" style="overflow: hidden"
                                   @click="blank(item.txt)"
                                   v-for="item in $store.state.messages.appcontact.appimg1">
                                    <div class="contact_radius">
                                        <img :src="UrlSrc+item.src"/>
                                    </div>
                                </a>
                            </div>
                        </div>
                        <div class="info-list">
                            <p>{{$store.state.messages.contactList[0].infotitle}}{{$store.state.messages.contactList[1].infotitle}}{{$store.state.messages.contactList[2].infotitle}}</p>
                        </div>
                        <div class="bottom-container">
                            <div class="protocol-container">
                                <div class="protocol-distance" @click="goToAppPrivacy">
                                    <span>Privacy</span>
                                    <div class="bottom-line"></div>
                                </div>
                                <div style="padding: 10px 0">
                                    &
                                </div>
                                <div class="protocol-distance" @click="goToAppTerms">
                                    <span>Terms</span>
                                    <div class="bottom-line"></div>
                                </div>
                            </div>
                            <span class="footer">Copyright © 2018 IRIS Foundation Ltd. All rights reserved.</span>
                        </div>
                    </div>
                </div>
            </div>
            <div class="wechat" v-show="wechatIs" @click="wechatIs=false">
                <div class="wechat_warp">
                    <img src="../assets/wechat.jpg" class="wechat_img"/>
                    <div class="wechat_title">
                        Get more
                    </div>
                    <div class="wechat_txt">
                        office info
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script type="text/ecmascript-6">
    import $ from 'jquery'
    import {mapState} from 'vuex'
    import CompCollaborationItem from '@/components/modules/collaborationItem.vue'
    import axios from "axios"
    import message from '../common/message';
    let Reveal
    if (process.env.VUE_ENV === 'client') {
        Reveal = require('reveal.js')
    }
    export default {
        name: "app",
        components: {CompCollaborationItem},
        data() {
            return {
                list: [
                    {is: true},
                    {is: false},
                    {is: false},
                    {is: false},
                ],
                menuIs: false,
                wechatIs: false,
                path: this.$route.path,
                mailaddress:"",
                showerr: false,
                links:message[this.$store.state.lang=='CN'?'cn':'en'].head.txt,
                subscription: this.$store.state.messages.submit.Subscribe,
                active:false
            }
        },
        methods: {
            handleSwipeLink(index){
                let mainnetModuleIndex = 0;
                if(index === mainnetModuleIndex){
                    this.$router.push('/mainnet/app');
                }
            },
            skipMainnet(){
                this.$router.push('/mainnet/app');
            },
            skipTestNet(){
                this.$router.push('/testnets/app');
            },
            imgChange(index, oldIndex) {
                this.$store.state.messages.logo.forEach(v => {
                    v.active = false;
                });
                this.$store.state.messages.logo[index].active = true
            },
            img(src) {
                return 'app/' + src;
            },
            txtShow(index) {
                this.list.forEach(v => {
                    v.is = false;
                })
                this.list[index].is = true;
            },
            blank(item) {
                if (item == 'Wechat') {
                    this.wechatIs = true;
                }
            },
            goToAppPrivacy(){
                this.$router.push({path: '/appPrivacy'})
            },
            goToAppTerms(){
                this.$router.push({path: '/appTerms'})
            },
            toHome(){
                let appHomeDomOffsetTop = 0;
                this.scroll(appHomeDomOffsetTop)
            },
            gotoCommunity(){
                this.$router.push({path: '/community'})
            },
            roll() {
                this.is = false;
                if (document.getElementById(this.$route.hash)) {
                    this.scroll(document.getElementById(this.$route.hash).offsetTop - 100)
                }
            },
            jump(){
                //解决锚点点击一次以后滚动效果不生效的问题
                this.scroll(346)
            },
            closeMenu(){
                this.menuIs = false;
            },
            scroll(top) {
                $('html,body').animate({
                        scrollTop: top
                    }, 500
                );
            },
            commitMaile(){
                let address =  /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
                if(address.exec(this.mailaddress)){
                    this.showerr = false;
                }else {
                    this.showerr = true;
                    let _this = this;
                    setTimeout(function () {
                        _this.showerr = false;
                    },2000)
                    return
                }
                axios({
                    method: 'post',
                    url:"/",
                    data: {
                        email:this.mailaddress,
                    }
                }).then((data)=>{
                    if(data.data.title == "Member Exists"){
                        this.subscription = this.$store.state.messages.submit.success;
                        let _this = this;
                        setTimeout(function () {
                            _this.subscription = _this.$store.state.messages.submit.Subscribe;
                            _this.mailaddress = "";
                            this.showerr = false;
                        },2000)
                    }
                })
                .catch((e)=>{
                })
            }
        },

        computed: {
            ...mapState({
                collaboration_title: state=>state.messages.collaboration.title,
                collaboration_core: state=>state.messages.collaboration.core,
                collaboration_strategy: state=>state.messages.collaboration.strategy,
                collaboration_ecosystem: state=>state.messages.collaboration.ecosystem,
                collaboration_investment: state=>state.messages.collaboration.investment,
                collaboration_counsel: state=>state.messages.collaboration.counsel,
            })
        },
        mounted: function () {
            this.path = this.$route.path
            this.$store.state.messages.head.txt.forEach(v => {
                v.href = v.href.substr(1, v.href.length)
            });
            this.roll();
            this.active = true;
        },
        watch: {
            '$route': 'roll'
        }
    }
</script>

<style scoped lang='less'>
    @import "../assets/style/newApp.less";
</style>