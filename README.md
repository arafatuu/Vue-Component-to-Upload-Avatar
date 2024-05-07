## Avatar Uploader Component in vue
This `AvatarUploader.vue` component is used for upload avatar of user profile with preview that enhance user experience.

### Usage
You can just import the component inside your page and reuse it. Assume `Profile.vue` is your main page where you want to use this component.

### Way to import
# In your parent vue page
- import the component

```
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
```

- Assign the component inside your template (Props takes the previous path of avatar)

```
<template>
    <div class="card">
        <div class="card-body pt-4 d-flex flex-column align-items-center">
            <!-- Give the previous avatar path as props , you may give  (path of avatar or '' or null ) -->
            <AvatarUploader :avatar="profileInfo.avatar" :withBtn="false"/> 
           <!-- Others logic may be added -->
        </div>
    </div>
</template>

```

- Props description
  - avatar : Get previous avatar path
  - withBtn: if you need upload button after upload an avatar , make it true otherwise false.

Great! Thanks for using it.

### Author
- Md. Arafat Rahman
- Email: arafat.r.riseuplabs@gmail.com