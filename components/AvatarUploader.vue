<template>
    <div>
        <form id="avatar-form">
            <input type="file" ref="fileInput" @change="handleFileChange" style="display: none" accept="image/*">
            <div class="avatar-container" @click="triggerFileInput">
                <img :src="avatarPreview" alt="Avatar" class="avatar-image" name="avatar">
                <div class="overlay">
                    <i class="fas fa-camera"></i>
                    <span>Change Photo</span>
                </div>
            </div>
            <div class="d-flex my-4" v-if="isUpload">
                <div class="btn btn-sm btn-danger mx-auto" @click="cancelAvatar">Cancel</div>
                <div class="btn btn-sm btn-success mx-auto" @click="uploadAvatar">Upload</div>
            </div>
        </form>
    </div>
    <div class="text-danger" v-if="validationErrors.avatar">
        {{ validationErrors . avatar }}
    </div>
</template>

<script>
    export default {
        props: {
            avatar: {
                type: String,
                default: null,
            },
            withBtn: {
                type: Boolean,
                default: true,
            }
        },
        data() {
            return {
                form: {
                    avatar: null,
                },
                isUpload: false,
                validationErrors: [],
                setting: {
                    withBtn: true,
                }

            };
        },
        watch: {
            avatar: {
                handler(newVal) {
                    this.form.avatar = newVal;
                },
                immediate: true,
            },
            withBtn: {
                handler(newVal){
                    this.setting.withBtn = newVal;
                },
            immediate: true,
            }
        },
        computed: {
            avatarPreview() {
                if (this.form.avatar instanceof File) {
                    return URL.createObjectURL(this.form.avatar);
                } else if (typeof this.form.avatar === 'string' && this.form.avatar) {
                    return '../storage/' + this.form.avatar;  // It depend on your file System
                }
                return 'https://thinksport.com.au/wp-content/uploads/2020/01/avatar-.jpg';
            }
        },

        methods: {
            triggerFileInput() {
                this.$refs.fileInput.click();
            },
            handleFileChange(event) {
                this.form.avatar = event.target.files[0] || null;
                if(this.setting.withBtn){
                    this.isUpload = true;
                }else{
                    this.uploadAvatar();
                }
            },
            uploadAvatar() {
                if (!(this.form.avatar instanceof File)) return;
                let formData = new FormData();
                formData.append('avatar', this.form.avatar);
                axios.post('your api url to upload', formData)
                    .then((res) => {
                        //Write you logic when upload successful
                        this.isUpload = false;
                    })
                    .catch(error => {
                        //Write you logic when upload got error
                        this.cancelAvatar();
                    });
            },
            cancelAvatar() {
                this.form.avatar = this.avatar;
                this.isUpload = false;
            },

        },
    };
</script>

<style scoped>
    .avatar-container {
        position: relative;
        overflow: hidden;
        width: 150px;
        height: 150px;
        border-radius: 50%;
        cursor: pointer;
        border: 1px solid #6c757d;
    }

    .avatar-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .overlay {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background: rgba(0, 0, 0, 0.5);
        color: #fff;
        opacity: 0;
        transition: opacity 0.3s ease;
    }

    .avatar-container:hover .overlay {
        opacity: 1;
    }

    .overlay i {
        margin-bottom: 5px;
    }
</style>
