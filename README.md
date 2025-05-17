import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { MapPin, Search } from "lucide-react";
import { useState } from "react";

export default function CoffeeMapHome() {
  const [search, setSearch] = useState("");

  return (
    <div className="p-4 md:p-6 grid gap-6">
      <h1 className="text-2xl md:text-3xl font-bold text-center">نقشه هوشمند قهوه ایران</h1>
      <div className="flex flex-col md:flex-row items-center justify-center gap-3 md:gap-4">
        <Input
          placeholder="جستجو براساس شهر، نوع فعالیت یا برند..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
          className="w-full md:w-1/2"
        />
        <Button className="w-full md:w-auto">
          <Search className="mr-2 h-4 w-4" /> جستجو
        </Button>
      </div>

      <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
        <Card>
          <CardContent className="p-4">
            <h2 className="font-semibold text-lg md:text-xl">برشته‌کاری قهوه سورنا</h2>
            <p className="text-sm text-muted-foreground">تهران - تخصص در قهوه‌های عربیکا</p>
            <div className="flex items-center mt-2 text-sm text-primary">
              <MapPin className="h-4 w-4 mr-1" /> تهران، خیابان انقلاب
            </div>
          </CardContent>
        </Card>

        <Card>
          <CardContent className="p-4">
            <h2 className="font-semibold text-lg md:text-xl">تأمین‌کننده تجهیزات قهوه تکسان</h2>
            <p className="text-sm text-muted-foreground">شیراز - واردات برند لامارزوکو</p>
            <div className="flex items-center mt-2 text-sm text-primary">
              <MapPin className="h-4 w-4 mr-1" /> شیراز، بلوار معالی‌آباد
            </div>
          </CardContent>
        </Card>

        <Card>
          <CardContent className="p-4">
            <h2 className="font-semibold text-lg md:text-xl">کافه موج سوم باریستا</h2>
            <p className="text-sm text-muted-foreground">اصفهان - ارائه قهوه تخصصی و آموزش باریستا</p>
            <div className="flex items-center mt-2 text-sm text-primary">
              <MapPin className="h-4 w-4 mr-1" /> اصفهان، خیابان چهارباغ بالا
            </div>
          </CardContent>
        </Card>
      </div>

      <div className="mt-8">
        <h2 className="text-xl font-semibold mb-4 text-center">ثبت کسب‌وکار شما در نقشه</h2>
        <form className="grid gap-4 max-w-xl mx-auto">
          <Input placeholder="نام کسب‌وکار" />
          <Input placeholder="شهر / استان" />
          <Input placeholder="نوع فعالیت (مثلاً برشته‌کاری، واردکننده، کافه...)" />
          <Input placeholder="آدرس دقیق یا لینک مکان در گوگل" />
          <Input placeholder="شماره تماس یا ایمیل" />
          <Button type="submit">ثبت در نقشه</Button>
        </form>
      </div>
    </div>
  );
}
