<template>
  <div>
      <div v-for="(row, index) in rows" :key="index">
          {{ row }}
      </div>
  </div>
</template>

<script>
    export default {
        props: {
            data: {
                type: Object,
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
                        icon: './assets/instagram.png',
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
                    medium: { icon: './assets/medium.png', color: '#00ab6c' },
                    pinterest: { icon: './assets/pinterest.png', color: '#bd081c' },
                    spotify: { icon: './assets/spotify.png', color: '#1db954' },
                    twitch: { icon: './assets/twitch.png', color: '#6441a5' },
                    twitter: { icon: './assets/twitter.png', color: '#1da1f2' },
                    youtube: { icon: './assets/youtube.png', color: '#ff0000' },
                }
            }
        },
        computed: {
            sorted() {
                return this.data.sort((a, b) => b.followers > a.followers);
            },
            rows() {
                return this.data.map((item, index) => {
                    let _icon = this.iconMap[item.platform];

                    let rowData = {
                        icon: _icon.icon,
                        color: _icon.color,
                        count: item.followers,
                        gradient: item.platform === 'instagram'
                    };

                    if (index === 0) {
                        rowData.percent = 1;
                    } else {
                        rowData.percent = (item.followers * 100) / sorted[0].followers / 100;
                    }
                    return rowData;
                    });
            }
        }
    }
</script>

<style scoped>
</style>