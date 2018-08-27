<template>
<div>
  <div class="post-description-emoji" :class="[this.isEmoji? 'emojiactive':'']" @click='emojiShowOff'>🙂</div>
          <textarea 
        class="form-control"
        rows="3" id="postDescriptionTextarea"
        v-model="postDescriptionTextarea" 
        @focus="postBtnActionFocus"
        @blur="postBtnActionBlur"></textarea>
           <picker
            v-show='isEmoji'
            :set='set'
            :emojiSize='emojiSize'
            :sheetSize='sheetSize'
            :defaultSkin='defaultSkin'
            emoji="department_store"
           :showPreview='showPreview' 
           :perLine='perLine' 
           :color='color'
           :skin='skin'
           :showSkinTones='showSkinTones'
           :emojiTooltip='emojiTooltip'
           @select='select'
           :style="{'width': '319px', 'z-index': '1','position':  'absolute','top': '25px','right': '-150px'}"/>
</div>

</template>


<script>
import { Picker } from 'emoji-mart-vue'
export default{
  components:{
    Picker,
  },
   data: function() {
        return {
          isEmoji:false,
          color:'#e5483f',
          emojiSize: 24,
          sheetSize:32,
          perLine: 9,
          skin: 1,
          defaultSkin:1,
          native:true,
          emojiTooltip:true,
          showSkinTones:true,
          showPreview: true,
          set: 'emojione',
          hidden: false,
          currentEmoji: { id: '+1' },
          autoFocus: false,
          include: [],
          exclude: [],
          postDescriptionTextarea:''}
      },
      methods:{
         emojiShowOff(){
          this.isEmoji = !this.isEmoji
        },
     select (emoji) {
      this.insertAtCaret('postDescriptionTextarea',emoji.native);
    },
      postBtnActionFocus(txt){
        this.isEmoji = false;
      },
    postBtnActionBlur(){  
      if( this.postDescriptionTextarea.length == 0 && this.thumbimage.length==0){
      }

    },
    
    insertAtCaret(areaId,text) {
    var txtarea = document.getElementById(areaId);
		var scrollPos = txtarea.scrollTop;
		var strPos = 0;
		var br = ((txtarea.selectionStart || txtarea.selectionStart == '0') ? 
      "ff" : (document.selection ? "ie" : false ) );

		if (br == "ie") { 
		
			var range = document.selection.createRange();
			range.moveStart ('character', -txtarea.value.length);
      strPos = range.text.length;
      console.log(strPos);
		}
		else if (br == "ff") strPos = txtarea.selectionStart;
	 
    var front = (txtarea.value).substring(0,strPos);
    
    var back = (txtarea.value).substring(strPos,txtarea.value.length);
		this.postDescriptionTextarea = front+text+back;
	  
	},
    
      }
}

</script>
