<template>
	<div v-if="responseSuccess">
		<div class="list">
			<div class="list-header">
				<p>Select Video To Display </p>
				<hr>
			</div>
			<div class="list-body">
				<ol >
					<li class="item" v-for="item in Data.items" @click="playVideo(item.contentDetails.videoId)">
						<img :src="item.snippet.thumbnails.default.url" >
						<div class="title" >
							<p> {{item.snippet.title}} </p>
						</div>
						<div class="clear"></div>
					</li>
				</ol>
			</div>
			<div class="list-footer" v-if="responseSuccess">
				<hr>
				<button @click="previousPage">previous</button>
				<button @click="nextPage">next</button>
			</div>
		</div>
		<div class="video-player">
			<player :id="videoId"></player>
		</div>
	</div>
</template>

<script type="text/javascript">
import Player from './Player.vue';
import axios from 'axios';

export default {
	components: {
		player : Player
	},
  data: function () {
    return {
    	responseSuccess: false,
      Data: [],
      token: '',
      videoId:''
    }
  },
  methods: {
  	playVideo: function(id){
  		this.videoId = id;
  		console.log(id)
  	},
  	nextPage: function() {
  		this.token = this.Data.nextPageToken,
  		this.fetchData()
  	},
  	previousPage: function() {
  		this.token = this.Data.prevPageToken,
  		this.fetchData()
  	},
  	setStatus: function(status) {
  		if ( status == 200 ) this.responseSuccess = true ; 
  	},
    fetchData: function () {
      axios.get('https://www.googleapis.com/youtube/v3/playlistItems', {
			  params: {
			    pageToken:this.token,
			    maxResults: '10',
			    part: 'snippet,contentDetails',
			    playlistId: 'PL1FWK-sgJ9eljz7Tm5SSUcCt5sxmwoFlC',
			    key: 'AIzaSyB6nP9sj8qS41jUrJwWFUc22AGwcQiUuII'
			  }
			}).then((response) => {
				console.log(response),
        this.Data = response.data,
        this.videoId = response.data.items[0].contentDetails.videoId,
        this.setStatus(response.status)
      }, (error) => {
        console.log(error)
      })
    }
  },
  mounted: function () {
    this.fetchData()
  }
}
</script>

<style scoped>
.list {
	width: 40%;
  background-color: #555;
  color: #FFF;
  margin-right: 0;
  float: left;
}
.list-header p {
	font-size: 18px;
	text-transform: uppercase;
	text-align: left;
	margin-left: 25px;
}

.list .list-body {
	height: 400px;
	overflow-y: auto;
}
.list .list-body ol {
	list-style-type: none;
	padding: 0 10px;
	margin-top: 0;
}
.list .list-body .item {
	padding: 10px;
	border-bottom: 2px solid #000;
}

.list .list-body .item:hover {
	cursor: pointer;
	background-color: #777;
	border-bottom: 2px solid #FFF;
	color: #FFF;
}
.list .list-body .item img {
	width: 80px;
	height: 50px;
	float: left;
}
.list .list-body .item .title {
	display: inline;
	float: left;
	margin-left: 10px;
}

.list-footer button:hover {
	color: #FE0303;
}
.list-footer button {
	cursor: pointer;
  padding: 2px 25px 7px 25px;
  background-color: transparent;
  border: 0;
  color: #fff;
  text-transform: uppercase;
  font-size: 16px;
}
.list-footer button {
  outline: 0;
}
.list-footer button:nth-of-type(2) {
	float: right;
}
.video-player {
	width: 60%;
	height: 512px;
	float: left;
}
.clear {   
	clear: both;
}
::-webkit-scrollbar {
    width: 0px;
    background: transparent; 
}
</style>   



