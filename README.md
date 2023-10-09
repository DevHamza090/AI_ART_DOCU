# AI Art Generator Android App API Documentation

## Introduction
Welcome to the documentation for the AI Art Generator Android app API. This API allows you to integrate the AI art generation capabilities of the app into your own Android applications. You can use this API to generate artistic images based on user prompts and various styles. Please note that you need to obtain an API key to access this service.

## Base URL
The base URL for the API is:
```
https://com.example.base_url.com/api
```

## API Key
You must include your API key in each API request. The API key is used for authentication.

Example API Key:
```
SVe947kjkfRf72BARd
```

## Models
The AI Art Generator supports the following models for image generation:

1. `realisticVisionV51_v51VAE`
2. `dreamshaper_8`
3. `majicmixRealistic_betterV2V25`
4. `deliberate_v2`
5. `revAnimated_v122`
6. `cyberrealistic_v32`
7. `ghostmix_v20Bakedvae`
8. `leosamsMoonfilm_filmGrain20`
9. `layriel_v16`
10. `meinamix_meinaV11`
11. `epicrealism_pureEvolutionV4`
12. `neverendingDreamNED_v122BakedVae`
13. `aZovyaRPGArtistTools_v3`
14. `epicDiffusion_epicDiffusion11`
15. `ANYTHING_MIDJOURNEY_V_4.1`
16. `mdjrny-v4`

## Styles
You can apply different artistic styles to the generated images. The following styles are available:

1. `3D Model`
2. `Photographic`
3. `Neon Punk`
4. `Enhance`
5. `Cinematic`
6. `Analog Film`
7. `Anime`
8. `Comic Book`
9. `Craft Clay`
10. `Digital Art`
11. `Fantasy Art`
12. `Isometric Style`
13. `Line Art`
14. `Lowpoly`
15. `Origami`
16. `Pixel Art`
17. `Texture`

## API Endpoints

### `generateArt`
This endpoint is used to generate an artistic image based on the provided parameters.

#### Request
- **HTTP Method:** POST
- **Endpoint:** `/generate_image`

#### Parameters
- `dev_key` (String, required): Your API key for authentication.
- `prompt` (String, required): The user's prompt for generating the image.
- `model` (String, optional): The model to use for image generation (default: `realisticVisionV51_v51VAE`).
- `negative_prompt` (String, optional): A negative prompt to influence the generation (default: `glitch`).
- `styles` (String, required): The artistic style to apply to the image (default: `anime`).
- `width` (String, required): The width of the generated image(default: `512`) (max: `2000`) (width mush divided on `8`).
- `height` (String, required): The height of the generated image(default: `512`)(max: `2000`) (height mush divided on `8`).
- `seed` (String, required): Seed for randomization (default: `-1`).
- `cfg_scale` (String, required): Configuration scale(default: `7`)(`1-20`).
- `steps` (String, required): The number of steps for generation (default: `30`)(`1-40`).
- `enable_hr` (String, required): Enable high resolution (default: `False`)(`True`, `False`).

#### Response
- The response will contain the generated image file.

## Example API Request
Here's an example of how to make an API request using the `generateArt` endpoint:

```kotlin
val artApi = Retrofit.Builder()
    .baseUrl("https://com.example.base_url.com/api")
    .build()
    .create(ArtApi::class.java)

val call = artApi.generateArt(
    devKey = "YOUR_API_KEY",
    prompt = "Generate a beautiful landscape",
    width = "512",
    height = "512",
    cfgScale = "7",
    steps = "30"
)

call.enqueue(object : Callback<ResponseBody> {
    override fun onResponse(call: Call<ResponseBody>, response: Response<ResponseBody>) {
        if (response.isSuccessful) {
            // Handle the generated image file here
            val imageResponseBody = response.body()
            // Save or display the image as needed
        } else {
            // Handle API error
        }
    }

    override fun onFailure(call: Call<ResponseBody>, t: Throwable) {
        // Handle network or other failures
    }
})
```
