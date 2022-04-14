<template lang="">
    <div class="table_header" v-if="currentView === 'table'">
        <div class="table_data">編號</div>
        <div class="table_data">行政區域</div>
        <div class="table_data">鄉鎮區</div>
        <div class="table_data">商家</div>
        <div class="table_data">地址</div>
    </div>
    <div v-for="(item, key) in rawData" :key="key">
        <!-- list view -->
        <div name="listView" v-if="currentView === 'list'">
            <div class="list_wrapper" :class="item.BlogUrl ? 'has_url' : ''" @click="linkUrl(item.BlogUrl)">
                <div class="list_regions">
                    <div class="list_city">{{item.City}}</div>
                    <div class="list_town">{{item.Town}}</div>
                </div>
                <div class="list_details">
                    <div class="list_img_wrapper">
                        <img class="list_img" v-bind:src="item.PicURL" />
                    </div>
                    <p class="list_name">{{item.Name}}</p>
                    <p class="list_feature">{{item.FoodFeature}}</p>
                </div>
            </div>
        </div>

        <!-- table view -->
        <div v-if="currentView === 'table'" name="tableView">
            <div class="table_row" :class="item.BlogUrl ? 'has_url' : ''" @click="linkUrl(item.BlogUrl)">
                <div class="table_data">{{key+1}}</div>
                <div class="table_data">{{item.Name}}</div>
                <div class="table_data">{{item.City}}</div>
                <div class="table_data">{{item.Town}}</div>
                <div class="table_data">{{item.Address}}</div>
            </div>
        </div>

        <!-- card view -->
        <div v-if="currentView === 'card'" name="cardView" >
            <div class="card_wrapper" :class="item.BlogUrl ? 'has_url' : ''" @click="linkUrl(item.BlogUrl)">
                <img class="card_img" v-bind:src="item.PicURL" />
                <div class="card_content">
                    <div class="card_regions">
                        <div class="card_city">{{item.City}}</div>
                        <div class="card_town">{{item.Town}}</div>
                    </div>
                    <p>{{item.Name}}</p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        rawData: {
            type: Array
        }
    },
    data() {
        return {
            currentView: 'list'
        }
    },
    methods: {
        linkUrl(BlogUrl) {
            if (BlogUrl) {
                console.log(BlogUrl);
            } else {
                console.log('no-url');
            }
        }
    }
}
</script>
<style lang="">
    
</style>