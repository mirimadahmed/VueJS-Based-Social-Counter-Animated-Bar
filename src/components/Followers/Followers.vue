<template>
  <div class="followers">
      <div v-for="(row, index) in rows" :key="index" class="follower-item">
        <div class="item">
            <img :src="row.icon" alt="icon not found" class="icon" />
        </div>
        <row :row="row" :animate="animate" :duration="duration" />
      </div>
  </div>
</template>
<script>
    import Row from './Row.vue';
    export default {
        components:{
            Row,
        },
        props: {
            data: {
                type: Array,
                required: true,
            },
            duration: {
                type: Number,
                require: true,
            },
            animate: {
                type: Boolean,
                require: true,
            },
        },
        data() {
            return {
                iconMap: {
                    instagram: {
                        icon: require('./assets/instagram.png'),
                        color: [
                            '#833ab4',
                            '#c13584',
                            '#e1306c',
                            '#f56040',
                            '#f77737',
                            '#fcaf45',
                            '#ffdc80',
                        ],
                    },
                    medium: { icon: require('./assets/medium.png'), color: '#00ab6c' },
                    pinterest: { icon: require('./assets/pinterest.png'), color: '#bd081c' },
                    spotify: { icon: require('./assets/spotify.png'), color: '#1db954' },
                    twitch: { icon: require('./assets/twitch.png'), color: '#6441a5' },
                    twitter: { icon: require('./assets/twitter.png'), color: '#1da1f2' },
                    youtube: { icon: require('./assets/youtube.png'), color: '#ff0000' },
                }
            }
        },
        computed: {
            rows() {
                let sorted = this.data.sort((a, b) => b.followers - a.followers);
                return sorted.map((item, index) => {
                    let _icon = this.iconMap[item.platform];

                    let rowData = {
                        icon: _icon.icon,
                        color: _icon.color,
                        count: item.followers,
                        gradient: item.platform === 'instagram'
                    };

                    if (index === 0) {
                        rowData.percent = 100;
                    } else {
                        rowData.percent = (item.followers * 100) / sorted[0].followers;
                    }
                    return rowData;
                    });
            }
        },
        methods: {
            
        }
    }
</script>

<style scoped>
.followers{
    padding: 20px 100px 20px 100px;
}
.follower-item{
    height: 24px;
    margin-bottom:50px;
}
.icon{
    height: 40px;
    width: 40px;
}
.item{
    float: left;
    width: 10%;
}
</style>