/**
    回复评论组件
 */
 <template>
  <div class='reply'>
      <div>
          <span>{{replies.length}}</span>&nbsp;回复
      </div>
      <div v-for='(item,index) in replies' :key='item.id'>
         <!-- 用户信息 -->
         <router-link :to="'/user/'+item.author.loginname">
            <img :src="item.author&&item.author.avatar_url" alt="用户头像">
         </router-link>
         <div>
             <div class='info'>
                 <p>
                     <span>{{index+1}}楼&nbsp;</span>
                     <router-link :to="'/user/'+item.author.loginname">
                        {{item.author.loginname}}
                     </router-link>
                     <span>
                         &nbsp;
                         {{$moment(item.create_at).startOf('day').fromNow()}}
                     </span>
                 </p>
                 <span class='thumbs'>
                     <img v-if='item.ups.length' :src="require('@/assets/image/thumbs-up.svg')" alt="点赞">
                     {{item.ups.length !==0?item.ups.length:''}}
                 </span>
             </div>
             <!-- 评论内容 -->
             <p v-html='item.content'></p>
         </div>
      </div>
  </div>
 </template>
 
 <script>
  export default {
      name:'Reply',
      props:{
          replies:{
              default(){
                  return []
              },
              type:Array
          }
      },
    data () {
      return {
          
      }
    },
    components: {
 
    }
  }
 </script>
 
 <style lang='scss' scoped>
    .reply{
        width:100%;
        img{
            width:50px;
            height:50px;
            border-radius: 5px;
            margin-right: 15px;
        }
        > div{
            display: flex;
            border: 1px solid #ebedf0;
            border-bottom-width: 0;
            color: rgba(0,0,0,0.65);
            padding:10px 20px;
            > div{
                width: 100%;
                > p{
                    margin: 0;
                    width: 100%;
                    /deep/ img{
                        width:100%;
                    }
                }
                .info{
                    width: 100%;
                    display: flex;
                    align-items: center;
                    justify-content: space-between;
                    > p{
                        margin: 0;
                    }
                    .thumbs{
                        font-size: 15px;
                        display: flex;
                        align-items: center;
                        img{
                            width: 12px;
                            height: 15px;
                            margin-right: 5px;
                            transform: rotate(-15deg);
                        }
                    }
                }
            }
        }
        > div:first-child{
            color: rgba(0,0,0,0.85);
            font-weight: bold;
        }
        > div:last-child{
            border-bottom: 1px solid #ebedf0;
        }
    }
  
 </style>
 