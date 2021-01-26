---
title: Döviz kurlarını alma
description: Belirli bir ay için yabancı Exchange ücretleri alın.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770629"
---
# <a name="get-foreign-exchange-rates"></a><span data-ttu-id="1341b-103">Döviz kurlarını alma</span><span class="sxs-lookup"><span data-stu-id="1341b-103">Get foreign exchange rates</span></span>

<span data-ttu-id="1341b-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="1341b-104">Applies to:</span></span>

- <span data-ttu-id="1341b-105">İş ortağı API 'SI</span><span class="sxs-lookup"><span data-stu-id="1341b-105">Partner API</span></span>

<span data-ttu-id="1341b-106">Bu konu, belirli bir ay için yabancı Exchange tarifelerinin nasıl alınacağını açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="1341b-106">This topic explains how to get foreign exchange rates for a given month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1341b-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1341b-107">Prerequisites</span></span>

- <span data-ttu-id="1341b-108">[Iş ortağı API kimlik doğrulaması](api-authentication.md)bölümünde açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1341b-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="1341b-109">Bu senaryo yalnızca uygulama kullanıcı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1341b-109">This scenario only supports application user authentication.</span></span> <span data-ttu-id="1341b-110">Yalnızca uygulama henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1341b-110">Application-only is not yet supported.</span></span>
- <span data-ttu-id="1341b-111">Bu API Şu anda yalnızca iş ortaklarının şu rollerden birinde olması gereken Kullanıcı erişimini destekliyor: genel yönetici, Yönetim Aracısı veya satış Aracısı.</span><span class="sxs-lookup"><span data-stu-id="1341b-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>


## <a name="details"></a><span data-ttu-id="1341b-112">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="1341b-112">Details</span></span>

- <span data-ttu-id="1341b-113">Şu anda, Azure planı CSP yerel para birimleri için beklenen ücretleri hesaplamak üzere [Fiyat Tablosu API 'si al](get-a-price-sheet.md) ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1341b-113">Currently used with [get price sheet API](get-a-price-sheet.md) to calculate expected charges for Azure plan CSP local currencies.</span></span>
- <span data-ttu-id="1341b-114">Yabancı Exchange ücretleri, nakledildikleri tüm ay için doğru bir tutar.</span><span class="sxs-lookup"><span data-stu-id="1341b-114">Foreign exchange rates hold true for the entire month they are posted.</span></span>
- <span data-ttu-id="1341b-115">Azure plan [fiyatlandırması](pricing.md) hakkında daha fazla bilgi için [Azure plan fiyatlandırma belgelerinde](https://docs.microsoft.com/partner-center/azure-plan-price-list)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1341b-115">More information about Azure plan [pricing](pricing.md) can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="1341b-116">İş ortağı fiyatlandırması ve yabancı değişim oranı API 'Leri, [Iş Ortağı Merkezi SDK 'sının](https://docs.microsoft.com/partner-center/develop/get-started)bir parçası değildir.</span><span class="sxs-lookup"><span data-stu-id="1341b-116">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="1341b-117">Bu yöntem, sonuçları bir dosya akışı olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="1341b-117">This method returns results as a file stream.</span></span> <span data-ttu-id="1341b-118">Dosya akışı bir. csv dosyası ya da. csv 'nin zip ile sıkıştırılmış bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="1341b-118">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="1341b-119">Sıkıştırılmış dosyaları isteme hakkındaki ayrıntılar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1341b-119">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="1341b-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1341b-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1341b-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1341b-121">Request syntax</span></span>

| <span data-ttu-id="1341b-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1341b-122">Method</span></span>   | <span data-ttu-id="1341b-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1341b-123">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1341b-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="1341b-124">**GET**</span></span> | <span data-ttu-id="1341b-125"> https://api.partner.microsoft.com/v1.0/sales/fxrates(Month=' {month} ')/$value</span><span class="sxs-lookup"><span data-stu-id="1341b-125">https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='{month}')/$value</span></span>                                  |

### <a name="uri-required-parameters"></a><span data-ttu-id="1341b-126">URI gerekli parametreler</span><span class="sxs-lookup"><span data-stu-id="1341b-126">URI required parameters</span></span>

<span data-ttu-id="1341b-127">İstediğiniz sayıda yabancı döviz kurunu istemek için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1341b-127">Use the following path parameters to request the month of foreign exchange rates you want.</span></span>

| <span data-ttu-id="1341b-128">Ad</span><span class="sxs-lookup"><span data-stu-id="1341b-128">Name</span></span>                   | <span data-ttu-id="1341b-129">Tür</span><span class="sxs-lookup"><span data-stu-id="1341b-129">Type</span></span>     | <span data-ttu-id="1341b-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1341b-130">Required</span></span> | <span data-ttu-id="1341b-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1341b-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="1341b-132">Ay</span><span class="sxs-lookup"><span data-stu-id="1341b-132">Month</span></span>                      | <span data-ttu-id="1341b-133">string</span><span class="sxs-lookup"><span data-stu-id="1341b-133">string</span></span>   | <span data-ttu-id="1341b-134">Yes</span><span class="sxs-lookup"><span data-stu-id="1341b-134">Yes</span></span>       | <span data-ttu-id="1341b-135">YYYıMM biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1341b-135">Must be in YYYMM format.</span></span> <span data-ttu-id="1341b-136">Atlanırsa, varsayılan olarak geçerli ay olur.</span><span class="sxs-lookup"><span data-stu-id="1341b-136">If omitted defaults to current month.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="1341b-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1341b-137">Request headers</span></span>

- <span data-ttu-id="1341b-138">Daha fazla bilgi için bkz. [Iş ortağı Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="1341b-138">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="1341b-139">Yukarıdaki üst bilgilere ek olarak, dosyalar sıkıştırılmış bant genişliği ve indirme süreleriyle sıkıştırılmış olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="1341b-139">In addition to the above headers, files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="1341b-140">Dosyalar varsayılan olarak sıkıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="1341b-140">By default the files are not compressed.</span></span> <span data-ttu-id="1341b-141">Dosyaların sıkıştırılmış sürümlerini almak için aşağıdaki üst bilgi değerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1341b-141">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="1341b-142">Sıkıştırılan sayfaların yalnızca 2020 Nisan 'dan kullanılabildiğini, 2020 Nisan 'dan önceki tüm isteklerin yalnızca sıkıştırılmamış olarak kullanılabildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1341b-142">Realize that compressed sheets are only available from April 2020 onward, all requests prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="1341b-143">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="1341b-143">Header</span></span>                   | <span data-ttu-id="1341b-144">Değer Türü</span><span class="sxs-lookup"><span data-stu-id="1341b-144">Value Type</span></span>     | <span data-ttu-id="1341b-145">Değer</span><span class="sxs-lookup"><span data-stu-id="1341b-145">Value</span></span> | <span data-ttu-id="1341b-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1341b-146">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="1341b-147">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="1341b-147">Accept-Encoding</span></span>| <span data-ttu-id="1341b-148">string</span><span class="sxs-lookup"><span data-stu-id="1341b-148">string</span></span>   | <span data-ttu-id="1341b-149">Söndür</span><span class="sxs-lookup"><span data-stu-id="1341b-149">deflate</span></span>| <span data-ttu-id="1341b-150">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="1341b-150">Optional.</span></span> <span data-ttu-id="1341b-151">Atlanan dosya akışı sıkıştırmamışsa.</span><span class="sxs-lookup"><span data-stu-id="1341b-151">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="1341b-152">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1341b-152">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="1341b-153">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1341b-153">REST response</span></span>

<span data-ttu-id="1341b-154">Başarılı olursa, bu yöntem bir dosya akışı olarak yabancı Exchange ücretleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1341b-154">If successful, this method returns foreign exchange rates as a file stream.</span></span> <span data-ttu-id="1341b-155">Dosya akışı bir. csv dosyası ya da. csv 'nin zip ile sıkıştırılmış bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="1341b-155">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1341b-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1341b-156">Response success and error codes</span></span>

<span data-ttu-id="1341b-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1341b-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1341b-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1341b-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1341b-159">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1341b-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1341b-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1341b-160">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
