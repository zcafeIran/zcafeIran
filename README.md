"use client";

import { useState } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { MapPin, Search } from "lucide-react";
import Map, { Marker, Popup } from "react-map-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import { businesses } from "@/lib/businesses";

export default function Home() {
  const [search, setSearch] = useState("");
  const [formData, setFormData] = useState({
    name: "",
    city: "",
    type: "",
    address: "",
    contact: "",
  });
  const [selectedBusiness, setSelectedBusiness] = useState<null | any>(null);

  const filteredBusinesses = businesses.filter(
    (business) =>
      business.name.includes(search) ||
      business.city.includes(search) ||
      business.type.includes(search)
  );

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    if (!formData.name || !formData.city) {
      alert("لطفاً نام کسب‌وکار و شهر را وارد کنید.");
      return;
    }
    console.log("فرم ارسال شد:", formData);
    setFormData({ name: "", city: "", type: "", address: "", contact: "" });
  };

  return (
    <div className="min-h-screen bg-gray-100 p-4 md:p-6">
      <h1 className="text-2xl md:text-3xl font-bold text-center mb-6">
        نقشه هوشمند قهوه ایران
      </h1>
      <div className="w-full h-[400px] mb-6 rounded-lg overflow-hidden">
        <Map
          initialViewState={{ latitude: 35.6892, longitude: 51.3890, zoom: 5 }}
          style={{ width: "100%", height: "100%" }}
          mapStyle="mapbox://styles/mapbox/streets-v11"
          mapboxAccessToken={process.env.NEXT_PUBLIC_MAPBOX_TOKEN}
        >
          {filteredBusinesses.map((business) => (
            <Marker
              key={business.id}
              latitude={business.lat}
              longitude={business.lng}
              onClick={() => setSelectedBusiness(business)}
            >
              <MapPin className="h-6 w-6 text-red-500" />
            </Marker>
          ))}
          {selectedBusiness && (
            <Popup
              latitude={selectedBusiness.lat}
              longitude={selectedBusiness.lng}
              onClose={() => setSelectedBusiness(null)}
              closeOnClick={false}
            >
              <div className="p-2">
                <h3 className="font-semibold">{selectedBusiness.name}</h3>
                <p className="text-sm">{selectedBusiness.type}</p>
                <p className="text-sm">{selectedBusiness.address}</p>
              </div>
            </Popup>
          )}
        </Map>
      </div>
      <div className="flex flex-col md:flex-row items-center justify-center gap-3 md:gap-4 mb-6">
        <Input
          placeholder="جستجو بر اساس شهر، نوع فعالیت یا برند..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
          className="w-full md:w-1/2"
          aria-label="جستجوی کسب‌وکارهای قهوه"
        />
        <Button disabled={!search} className="w-full md:w-auto">
          <Search className="mr-2 h-4 w-4" /> جستجو
        </Button>
      </div>
      <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 mb-8">
        {filteredBusinesses.map((business) => (
          <Card key={business.id}>
            <CardContent className="p-4">
              <h2 className="font-semibold text-lg md:text-xl">
                {business.name}
              </h2>
              <p className="text-sm text-muted-foreground">{business.type}</p>
              <div className="flex items-center mt-2 text-sm text-primary">
                <MapPin className="h-4 w-4 mr-1" /> {business.address}
              </div>
            </CardContent>
          </Card>
        ))}
      </div>
      <div className="max-w-xl mx-auto">
        <h2 className="text-xl font-semibold mb-4 text-center">
          ثبت کسب‌وکار شما در نقشه
        </h2>
        <form onSubmit={handleSubmit} className="grid gap-4">
          <Input
            placeholder="نام کسب‌وکار"
            value={formData.name}
            onChange={(e) =>
              setFormData({ ...formData, name: e.target.value })
            }
          />
          <Input
            placeholder="شهر / استان"
            value={formData.city}
            onChange={(e) =>
              setFormData({ ...formData, city: e.target.value })
            }
          />
          <Input
            placeholder="نوع فعالیت (مثلاً برشته‌کاری، کافه...)"
            value={formData.type}
            onChange={(e) =>
              setFormData({ ...formData, type: e.target.value })
            }
          />
          <Input
            placeholder="آدرس دقیق"
            value={formData.address}
            onChange={(e) =>
              setFormData({ ...formData, address: e.target.value })
            }
          />
          <Input
            placeholder="شماره تماس یا ایمیل"
            value={formData.contact}
            onChange={(e) =>
              setFormData({ ...formData, contact: e.target.value })
            }
          />
          <Button type="submit">ثبت در نقشه</Button>
        </form>
      </div>
    </div>
  );
}
