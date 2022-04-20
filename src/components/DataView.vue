<template lang="">
    <div id="loading_wrapper" v-if="isLoading">
        <img id="loafing_indicator" src="../assets/images/loading.gif">
    </div>
    <div id="func_bar">
        <div id="region_filter">
            <div class="select_wrapper city">
                <select id="city_select"  @change="cityOnChange($event)">
                    <option value="0">請選擇行政區域</option>
                    <option v-for="(item, key) in regionData" :key="key" :value="item.name">{{item.name}}</option>
                </select>
            </div>
            <div class="select_wrapper town">
                <select id="town_select" @change="townOnChange($event)">
                    <option value="0">請選擇鄉鎮區</option>
                    <option v-for="(item, key) in filteredByCityData" :key="key" :value="item.name">{{item.name}}</option>
                </select>
            </div>
        </div>
        <div id="view_filter">
            <span id="view_filter_text">檢視模式：</span>
            <div id="view_filter_inner">
                <button class="view_btn" :class="{active : currentView==='list'}" @click="currentView = 'list'">
                    <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
                    <svg class="view_img" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="560.414px" height="560.415px" viewBox="0 0 560.414 560.415" style="enable-background:new 0 0 560.414 560.415;" xml:space="preserve">
                        <g>
                            <g>
                                <path d="M115.65,24.92H33.507C15.031,24.92,0,39.951,0,58.421v82.143c0,18.477,15.031,33.501,33.507,33.501h82.143
                                    c18.476,0,33.501-15.031,33.501-33.501V58.421C149.145,39.945,134.12,24.92,115.65,24.92z"/>
                                <path d="M526.908,24.92H212.205c-18.477,0-33.501,15.031-33.501,33.501v82.143c0,18.477,15.025,33.501,33.501,33.501h314.703
                                    c18.477,0,33.506-15.031,33.506-33.501V58.421C560.414,39.945,545.377,24.92,526.908,24.92z"/>
                                <path d="M115.65,205.632H33.507C15.031,205.632,0,220.663,0,239.133v82.143c0,18.476,15.031,33.5,33.507,33.5h82.143
                                    c18.476,0,33.501-15.024,33.501-33.5v-82.143C149.145,220.657,134.12,205.632,115.65,205.632z"/>
                                <path d="M526.908,205.632H212.205c-18.477,0-33.501,15.031-33.501,33.501v82.143c0,18.476,15.025,33.5,33.501,33.5h314.703
                                    c18.477,0,33.506-15.024,33.506-33.5v-82.143C560.414,220.657,545.377,205.632,526.908,205.632z"/>
                                <path d="M115.65,386.343H33.507C15.031,386.343,0,401.374,0,419.85v82.143c0,18.477,15.031,33.501,33.507,33.501h82.143
                                    c18.476,0,33.501-15.024,33.501-33.501V419.85C149.145,401.374,134.12,386.343,115.65,386.343z"/>
                                <path d="M526.908,386.343H212.205c-18.477,0-33.501,15.03-33.501,33.507v82.143c0,18.477,15.025,33.501,33.501,33.501h314.703
                                    c18.477,0,33.506-15.024,33.506-33.501V419.85C560.414,401.374,545.377,386.343,526.908,386.343z"/>
                            </g>
                        </g>
                    </svg>
                </button>
                <button class="view_btn" :class="{active : currentView==='table'}" @click="currentView = 'table'">
                    <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
                    <svg class="view_img" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="556.98px" height="556.98px" viewBox="0 0 556.98 556.98" style="enable-background:new 0 0 556.98 556.98;" xml:space="preserve">
                        <g>
                            <g>
                                <path d="M536.846,23.491H20.135C9.015,23.491,0,32.506,0,43.62v107.37c0,11.12,9.015,20.128,20.135,20.128h516.711
                                    c11.121,0,20.135-9.015,20.135-20.128V43.626C556.975,32.506,547.967,23.491,536.846,23.491z"/>
                                <path d="M536.846,204.68H20.135C9.015,204.68,0,213.694,0,224.809v107.369c0,11.12,9.015,20.129,20.135,20.129h516.711
                                    c11.121,0,20.135-9.015,20.135-20.129V224.809C556.975,213.688,547.967,204.68,536.846,204.68z"/>
                                <path d="M536.846,385.862H20.135C9.015,385.862,0,394.877,0,405.991V513.36c0,11.12,9.015,20.129,20.135,20.129h516.711
                                    c11.121,0,20.135-9.015,20.135-20.129V405.991C556.975,394.877,547.967,385.862,536.846,385.862z"/>
                            </g>
                        </g>
                    </svg>
                </button>
                <button class="view_btn" :class="{active : currentView==='card'}" @click="currentView = 'card'">
                    <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
                    <svg class="view_img" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="514.08px" height="514.08px" viewBox="0 0 514.08 514.08" style="enable-background:new 0 0 514.08 514.08;" xml:space="preserve">
                        <g>
                            <g>
                                <rect y="0.961" width="207.168" height="207.168"/>
                                <rect x="306.912" y="0.961" width="207.168" height="207.168"/>
                                <rect y="305.951" width="207.168" height="207.168"/>
                                <rect x="306.912" y="305.951" width="207.168" height="207.168"/>
                            </g>
                        </g>
                    </svg>
                </button>
            </div>
        </div>
    </div>
    <div v-if="!emptyResult">
        <div class="listView" name="listView" v-if="currentView === 'list'">
            <div class="item_wrapper" v-for="(item, key) in filteredByPageData" :key="key">
                <div class="list_wrapper " :class="item.Url ? 'has_url' : ''" @click="linkUrl(item.Url)">
                    <div class="list_region region_wrapper outside">
                        <div class="list_city region_city">{{item.City}}</div>
                        <div class="list_town region_town">{{item.Town}}</div>
                    </div>
                    <div class="list_details">
                        <div class="list_img_wrapper img_wrapper">
                            <img class="list_img img" v-bind:src="item.PicURL" />
                            <div class="img_mask"></div>    
                        </div>
                        <div class="list_details_inner">
                            <p class="list_name">{{item.Name}}</p>
                            <div class="list_region region_wrapper inside">
                                <div class="list_city region_city">{{item.City}}</div>
                                <div class="list_town region_town">{{item.Town}}</div>
                            </div>
                            <p class="list_feature">{{item.FoodFeature.replace(/&lt;br&gt;/g, '')}}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="tableView" name="tableView" v-if="currentView === 'table'">
            <div id="tableView_inner">
                <div id="table_header" class="table_row" v-if="currentView === 'table'">
                    <div class="table_data id">編號</div>
                    <div class="table_data city">行政區域</div>
                    <div class="table_data town">鄉鎮區</div>
                    <div class="table_data name">商家</div>
                    <div class="table_data addr">地址</div>
                </div>
                <div class="item_wrapper" v-for="(item, key) in filteredByPageData" :key="key">
                    <div class="table_row" :class="item.Url ? 'has_url' : ''" @click="linkUrl(item.Url)">
                        <div class="table_data id">{{key+1}}</div>
                        <div class="table_data city">{{item.City}}</div>
                        <div class="table_data town">{{item.Town}}</div>
                        <div class="table_data name">{{item.Name}}</div>
                        <div class="table_data addr" :title="item.Address">{{item.Address}}</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="cardView" name="cardView" v-if="currentView === 'card'">
            <div class="item_wrapper" v-for="(item, key) in filteredByPageData" :key="key">
                <div class="card_wrapper" :class="item.Url ? 'has_url' : ''" @click="linkUrl(item.Url)">
                    <div class="img_wrapper" :style="{'background-image': 'url('+item.PicURL+')'}">
                        <div class="img_mask"></div>
                    </div>
                    <div class="card_content">
                        <div class="card_region region_wrapper">
                            <div class="card_city region_city">{{item.City}}</div>
                            <div class="card_town region_town">{{item.Town}}</div>
                        </div>
                        <p class="card_name">{{item.Name}}</p>
                        <p class="card_feature">{{item.FoodFeature.replace(/&lt;br&gt;/g, '')}}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="empty_result" v-if="emptyResult">無搜尋結果</div>

    <div id="pagination" v-if="!emptyResult">
        <p id="pagination_text">美食頁次 {{this.page}}/{{this.totalPage}}</p>
        <div id="pagination_inenr">
            <button class="page_btn" :class="{active:this.page==n}" v-for="n in this.totalPage" :key="n" @click="setPage(n)">{{n}}</button>
        </div>
    </div>
    
</template>

<script>

export default {
    props: {
        rawData: {
            type: Array
        },
        regionData: {
            type: Array
        }
    },
    data: () => ({
        isLoading: true,
        emptyResult: false,
        currentView: 'list',
        selectedCity: '',
        filteredByCityData: [],
        filteredByTownData: [],
        filteredRawData: [],
        filteredByPageData: [],
        page: 1,
        totalPage: 0
    }),
    methods: {
        cityOnChange(event) {
            document.getElementById('town_select').selectedIndex = 0;
            let selectedCity = event.target.value;
            this.selectedCity = selectedCity;
            this.page = 1;

            // filter the Town selector
            let filteredRegionData = this.regionData.filter(function(item) {
                return item.name == selectedCity;
            });

            if(this.selectedCity === '0') {
                this.emptyResult = false;
                this.filteredRawData = this.rawData;
                this.filteredByCityData = [];
                this.setPage(1);
            } else {
                
                this.filteredByCityData = filteredRegionData[0].districts;

                // filter the result data view
                let filteredRawData = this.rawData.filter(function(item) {
                    return item.City == selectedCity;
                });

                if(filteredRawData.length == 0) {
                    this.emptyResult = true;
                } else {
                    this.emptyResult = false;
                    this.filteredRawData = filteredRawData;
                    this.setPage(1);
                }
            }
        },
        townOnChange(event) {
            this.page = 1;
            let selectedTown = event.target.value;
            let selectedCity = this.selectedCity;
            if(selectedTown === '0') {
                this.emptyResult = false;
                this.page = 1;
                let filteredRawData = this.rawData.filter(function(item) {
                    return item.City == selectedCity;
                });
                this.filteredRawData = filteredRawData;
            } else {
                // filter the result data view
                let filteredRawData = this.rawData.filter(function(item) {
                    return item.Town == selectedTown;
                });

                if(filteredRawData.length == 0) {
                    this.emptyResult = true;
                    this.page = 1;
                } else {
                    this.emptyResult = false;
                    this.filteredRawData = filteredRawData;
                    this.setPage(1);
                }
            }
        },
        setPage(event) {
            this.page = event;
            this.totalPage = Math.ceil(this.filteredRawData.length/10);
            // update page of items
            let offset = (this.page - 1)*10;
            this.filteredByPageData = this.filteredRawData.slice(offset, offset+10);
            window.scrollTo(0,0)
        },
        linkUrl(Url) {
            if (Url) {
                window.open(Url, '_blank');
            }
        },
    },
    mounted() {
        this.filteredRawData = this.rawData;
        this.totalPage = Math.ceil(this.filteredRawData.length/10);
        this.setPage(1);
        this.isLoading = false;
    }
}
</script>
<style lang="scss" scoped>
#loading_wrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: $white;
    z-index: 10;

    #loafing_indicator {
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: -33px;
        margin-left: -33px;
    }
}
.select_wrapper {
    display: block;
    width: 100%;
    height: auto;
    position: relative;
    margin-right: $spacing;
    margin-bottom: $spacing;
    padding-right: $spacing;
    background-color: #CFD0D1;

    &:after {
        content: '\25BE';
        position: absolute;
        top: 7px;
        right: 10px;
        font-size: 16px;
        margin-left: 10px;
    }

    @media (min-width: 768px) {
        display: inline-block;
        width: auto;
        margin-bottom: 0;
        padding-right: 25px;

        &:after {
            right: 8px;
        }
    }

    select {
        width: 100%;
        height: auto;
        padding: 10px;
        font-size: 16px;
        font-weight: 400;
        background: none;
        color: #333;

        @media (min-width: 768px) {
            width: auto;
        }
    }
}

#func_bar {
    overflow: hidden;
    padding-bottom: $spacing*2;
    font-wieght: 400;
    letter-spacing: 0.05em;

    #view_filter {
        display: block;
        text-align: center;
        color: #999;

        @media (min-width: 768px) {
            margin-top: 8px;
            margin-left: $spacing*3;
            float: right;
        }

        #view_filter_text {
            display: inline-block;
            vertical-align: middle;
        }

        #view_filter_inner {
            display: inline-block;
            vertical-align: middle;

            .view_btn {
                display: inline-block;
                margin-top: 1px;
                vertical-align: middle;
                background: transparent;

                &:hover {
                    cursor: pointer;
                }

                .view_img {
                    width: 20px;
                    height: 20px;
                    fill: #999;
                }

                &.active {

                    .view_img {
                        fill: #333;
                    }
                }
            }
        }
    }

    #region_filter {
        display: block;
        overflow: hidden;

        @media (min-width: 768px) {
            float: left;
        }
    }
}

.listView {

    .item_wrapper {

        &:hover {

            .img_wrapper {

                .img {
                    transform: scale(1.3);
                }

                .img_mask {
                    opacity: 0;
                }
            }
        }

        .img_wrapper {
            position: relative;
            overflow: hidden;
            line-height: 1;
        
            .img {
                width: 100%;
                transition: transform 0.5s ease-in-out;
            }
        
            .img_mask {
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: #000;
                opacity: 0.3;
                transition: opacity .5s ease-in-out;
            }
        }
    }

    .list_wrapper {
        overflow: hidden;
        margin-bottom: $spacing*2;

        &.has_url {

            .list_name {
                color: $blue;
            }
        }

        .list_region {
            
            &.outside {
                display: none;
                float: left;
                    
                .list_city {
                    margin-bottom: $spacing/2;
                }

                .list_town {
                    display: block;
                    width: 16px;
                    margin-left: 30px;
                    text-align: right;
                }
            }

            &.inside {
                display: block;
            }

            @media (min-width: 768px) {

                &.outside {
                    display: block;
                }

                 &.inside {
                     display: none;
                 }
            }
        }

        .list_details {
            overflow: hidden;
            padding: 15px;
            background-color: $white;
            box-shadow: 2px 2px 10px 1px #CCC;

            .list_img_wrapper {
                width: 100%;
                height: auto;
                margin-bottom: 15px;

                .list_img {
                    width: 100%;
                }
                
                @media (min-width: 768px) {
                    width: 200px;
                    float: left;
                    margin-bottom: 0;
                    margin-right: 15px;
                }
            }

            .list_details_inner {

                .list_name {
                    margin-bottom: 10px;
                    font-size: 28px;
                    font-weight: 500;
                }

                .list_feature {
                    display: -webkit-box;
                    overflow: hidden;
                    text-overflow: ellipsis;
                    font-weight: 300;
                    -webkit-line-clamp: 3;
                    -webkit-box-orient: vertical;
                }

                @media (min-width: 768px) {
                    overflow: hidden;
                }
            }
        }
    }
}



.tableView {
    overflow: auto;
    
    #tableView_inner {
        overflow: scroll;
        overflow-y: hidden;
        min-width: 910px;
        margin-bottom: 20px;

        @media (min-width: 1024px) {
            min-width: 40%;
        }
    }

    .table_row {
        overflow: hidden;

        .table_data {
            float: left;
            padding: $spacing;
            border-right: 1px solid $table_border_color;
            color: #666;
            font-size: 14px;
            font-weight: 300;

            &:last-of-type {
                border: none;
            }

            &.id {
                width: 8%;
                text-align: right;
            }

            &.city {
                width: 12%;
            }

            &.town {
                width: 11%;
            }

            &.name {
                width: 32%;
            }

            &.addr {
                width: 37%;
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
            }
        }
    }

    #table_header {
        overflow: hidden;
        border: 1px solid $table_border_color;
        background-color: #EAEBED;
        background: linear-gradient(rgb(248, 250, 251), rgb(231, 231, 231));

        .table_data {
            text-align: center;
        }
    }

    .item_wrapper {
        border: 1px solid $table_border_color;
        border-top: none;

        &:nth-child(even) {
            background-color: $white;
        }

        &:hover {
            background-color: #EBF1F5;
        }
    }
}

.cardView {

    .card_wrapper {
        position: relative;
    }

    .item_wrapper {
        position: relative;
        margin-bottom: $spacing*2;

        @media (min-width: 768px) {
            width: 50%;
            float: left;
            padding-right: $spacing;

            &:nth-child(even) {
                padding-right: 0;
                padding-left: $spacing;
            }
        }

        &:hover {

            .card_wrapper {

                .img_wrapper {
                    background-size: 130%;
                }
            }

            .card_content {

                .card_feature {
                    display: -webkit-box;
                }
            }
        }

        .img_wrapper {
            position: relative;
            width: 100%;
            min-height: 200px;
            background-repeat: no-repeat;
            background-size: 100% auto;
            background-position: center center;
            transition: background-size 0.5s ease-in-out;

            .img_mask {
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: linear-gradient(transparent, rgba(0, 0, 0, 0.7));
            }
        }

        .card_content {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: auto;
            padding: 15px;
            color: $white;

            .card_region {
                font-size: 14px;

                .card_town {
                    font-size: 16px;
                    font-style: italic;
                }
            }

            .card_feature {
                display: none;
                overflow: hidden;
                position: relative;
                margin-top: 10px;
                padding-top: 10px;
                text-overflow: ellipsis;
                font-weight: 300;
                -webkit-line-clamp: 2;
                -webkit-box-orient: vertical;

                &:before {
                    content: '';
                    position: absolute;
                    top: 0;
                    left: 0;
                    width: 50px;
                    height: 2px;
                    background-color: $white;
                }
            }
        }
    }
}

#pagination {
    display: block;
    overflow: hidden;
    width: 100%;

    #pagination_text {
        display: none;
        float: left;
        margin-top: 7px;
        margin-right: $spacing*2;
        
        @media (min-width: 768px) {
            display: block;
        }
    }

    #pagination_inenr {
        display: block;
        overflow: hidden;

        @media (min-width: 768px) {
            text-align: right;
        }

        .page_btn {
            margin-bottom: $spacing/2;
            margin-right: $spacing/2;
            padding: 7px $spacing;
            font-size: 18px;
            line-height: 1;
            color: #BBB;
            background-color: #DDD;

            &:last-of-type {
                margin-right: 0;
            }

            &:hover {
                cursor: pointer;
                color: $white;
                background-color: $blue;
            }

            &.active {
                color: $white;
                background-color: $blue;
            }
        }
    }
}
</style>