<template>
    <div class="card">
        <div class="card-body pt-4 d-flex flex-column align-items-center">
            <!-- Give the previous avatar path as props , you may give  (path of avatar or '' or null ) -->
            <AvatarUploader :avatar="profileInfo.avatar"/> 
           <!-- Others logic may be added -->
        </div>
    </div>
</template>
<script>
import AvatarUploader from '../components/AvatarUploader.vue';
export default {
   
    components: {
        AvatarUploader,
    } ,
    data() {
        return {
            profileInfo: {
                avatar: 'Set your previous avatar',
            },
        }
    }
}
</script>
