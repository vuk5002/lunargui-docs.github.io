# Vulkan for Lunar tutorial
<div style="
    background-color:#004173;
    border-left: 5px solid #0066cc;
    color: #ffffff;
    border-radius: 12px;
    padding: 16px;
    margin: 16px 0;
    box-shadow: 0 2px 8px rgba(255, 255, 255, 0.1);
">
<span style="font-size:22px ; font-weight: bold;">🔷 IMPORTANT</span>

<span style="font-size:18px ; font-weight: bold;">Make sure you have knowledge of Vulkan before reading</span>
</div>

<div style="
    background-color:#004173;
    border-left: 5px solid rgb(255, 0, 0);
    color: #ffffff;
    border-radius: 12px;
    padding: 16px;
    margin: 16px 0;
    box-shadow: 0 2px 8px rgba(255, 255, 255, 0.1);
">
<span style="font-size:22px ; font-weight: bold;">🔷 IMPORTANT</span>

<span style="font-size:18px ; font-weight: bold;">Vulkan is still in development and unfinished</span>


</div>

<span style="font-size:18px ; font-weight: bold;">Welcome, in this article you will learn how to start using Vulkan for Lunar programs, by the end of this we will make a triangle using Vulkan, but first lets start with most basic vulkan functions</span>

<span style="font-size:18px ; font-weight: bold;">If you are using LEX+ as an option in LStudio sometimes it fucks up and doesnt know what program type it is, I recommend assigning it manually with lexcreate command</span>

## vkCreateInstance
[Manual page](https://registry.khronos.org/vulkan/specs/latest/man/html/vkCreateInstance.html)
<br>
<span style="font-size:18px ; font-weight: bold;">job of vkCreateInstance is to initializes Vulkan so we can actually use its functions, the signature for it is ofc the same as found at 
registry.khronos.org, </span>

```c
// Provided by VK_VERSION_1_0
VkResult vkCreateInstance(
    const VkInstanceCreateInfo*                 pCreateInfo,
    const VkAllocationCallbacks*                pAllocator,
    VkInstance*                                 pInstance);
```

<span style="font-size:18px ; font-weight: bold;">To initialize a Vulkan instance we need to fill out VkApplicationInfo and VkInstanceCreateInfo structs, this is an example</span>

```c
VkApplicationInfo app_info = {0};
app_info.sType = VK_STRUCTURE_TYPE_APPLICATION_INFO; // type of the structure (APP INFO)
app_info.pApplicationName = "Example Vulkan program"; // program name
app_info.applicationVersion = VK_MAKE_VERSION(1, 0, 0); // program version
app_info.pEngineName = "No Engine"; // if you are making your custom engine fill this out
app_info.engineVersion = VK_MAKE_VERSION(1, 0, 0); // version of your engine
app_info.apiVersion = VK_API_VERSION_1_0; // tells what api version will our program use, in this case Vulkan 1.0
```

<span style="font-size:18px ; font-weight: bold;">VkInstanceCreateInfo struct is the one that gets passed to vkCreateInstance but you need app info for it.</span>

```c
VkInstanceCreateInfo create_info = {0};
create_info.sType = VK_STRUCTURE_TYPE_INSTANCE_CREATE_INFO; // type of the structure
create_info.pApplicationInfo = &app_info; // app info we created earlier
create_info.enabledExtensionCount = 0; // read more below
create_info.ppEnabledExtensionNames = NULL; // read more below

```
<span style="font-size:18px ; font-weight: bold;">enabledExtensionCount is how much extensions we want enabled in our program, and ppEnabledExtensionNames are the extensions to enable.
 You can manually pass them: </span>

```c
const char* extensions[] = {...}
...
create_info.enabledExtensionCount = n;
create_info.ppEnabledExtensionNames = extensions;
```
<span style="font-size:18px ; font-weight: bold;">or trough loops to enable every supported...</span>
<span style="font-size:18px ; font-weight: bold;">We can finally create a vulkan instance: </span>

```c
VkInstance instance;
VkResult result = vkCreateInstance(&create_info, NULL, &instance);
if(result != VK_SUCCESS){ // PLEASE do error checking
    // error out
    return -1;
}
// if we get to here instance created
```

## vkEnumeratePhysicalDevices
[Manual page](https://registry.khronos.org/vulkan/specs/latest/man/html/vkEnumeratePhysicalDevices.html)

<span style="font-size:18px ; font-weight: bold;">job of vkEnumeratePhysicalDevices is to as its name says, enumerate all GPUs inside the computer, </span>

```c
// Provided by VK_VERSION_1_0
VkResult vkEnumeratePhysicalDevices(
    VkInstance                                  instance,
    uint32_t*                                   pPhysicalDeviceCount,
    VkPhysicalDevice*                           pPhysicalDevices);
```

<span style="font-size:18px ; font-weight: bold;">theres 2 steps of using it, enumerating gpus (counting them), and fetching the gpu</span>
<div style="
    background-color:#004173;
    border-left: 5px solid rgb(255, 0, 0);
    color: #ffffff;
    border-radius: 12px;
    padding: 16px;
    margin: 16px 0;
    box-shadow: 0 2px 8px rgba(255, 255, 255, 0.1);
">
<span style="font-size:22px ; font-weight: bold;">🔷 IMPORTANT</span>

<span style="font-size:18px ; font-weight: bold;">If you have a GPU installed and your gpu count is at 0 that means Vulkan isnt supported by your gpu</span>


</div>

```c
int gpuc = 0; // number of GPUS available with Vulkan support
VkResult result = vkEnumeratePhysicalDevices(instance, &gpuc, NULL);
if (gpuc <= 0) {
    // error out
    return -1;
}
```
<span style="font-size:22px ; font-weight: bold;">Rare chance you can get hit with VK_INCOMPLETE code, THIS DOENST MEAN IT FAILED, it means that not all GPUs could be enumerated</span>

<span style="font-size:22px ; font-weight: bold;">once we get all gpus with vulkan support, we can fetch them. Most programs select the count to be 1 (aka only fetch FIRST gpu in the list),
or you can fetch ALL available gpus</span>

```c
n_gpus = 1; // we want first gpu, if you wanted multiple you wouldnt add this line
VkPhysicalDevice gpu = {0}; // represents a physical gpu, used later
VkResult result = vkEnumeratePhysicalDevices(instance, &n_gpus, &gpu);
// error if some shit is returned
```

